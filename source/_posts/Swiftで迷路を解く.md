---
title: Swiftで迷路を解く
date: 2021-02-20 22:28:40
tags: Swift
---
## 目的
- Swiftの勉強

## 制作時間
- 4時間

## コード
```swift
import UIKit

var targetMaze = [
    ["#","S","#","#","#","#","#","#","#","#","#"],
    ["#"," ","#","#","#","#","#","#"," ","#","#"],
    ["#"," "," "," "," ","#","#"," "," ","#","#"],
    ["#"," ","#","#"," "," "," "," ","#","#","#"],
    ["#","#","#","#"," ","#","#","#","#","#","#"],
    ["#"," "," "," "," ","#"," "," "," ","#","#"],
    ["#"," ","#","#","#","#"," ","#"," ","#","#"],
    ["#"," ","#","#","#","#"," ","#"," ","#","#"],
    ["#"," "," "," "," "," "," ","#"," ","#","#"],
    ["#","#","#","#","#","#","#","#","G","#","#"]
]

enum MapType:String
{
    case Start = "S"
    case Goal = "G"
    case Wall = "#"
    case Root = "+"
}

struct Vec2:Equatable{
    var X:Int = 0
    var Y:Int = 0
}

struct Direction
{
    var Now:Vec2

    var Up:Vec2?
    var Down:Vec2?
    var Right:Vec2?
    var Left:Vec2?
}

func CheckRoad(maze:[[String]],pos:Vec2?,beforPos:Vec2,maxPos:Vec2,checkType:MapType)-> Direction?
{
    if(pos == nil) {
        return nil
    }

    //  上,右,下,左
    var retPos:Direction = Direction(Now:pos!,Up:nil,Down: nil,Right: nil,Left: nil)

    //  上下左右の座標を取得
    let minusY = retPos.Now.Y - 1
    let plusY = retPos.Now.Y + 1
    let minusX = retPos.Now.X - 1
    let plusX = retPos.Now.X + 1

    // マップ内かチェック
    if(minusY >= 0){
        retPos.Down = Vec2()
    }
    if(plusY < maxPos.Y){
        retPos.Up = Vec2()
    }
    if(minusX >= 0){
        retPos.Left = Vec2()
    }
    if(plusX < maxPos.X){
        retPos.Right = Vec2()
    }

    //  壁があるかチェック
    if(retPos.Down == Vec2() &&
        (maze[minusY][retPos.Now.X] != checkType.rawValue) &&
        beforPos != Vec2(X: retPos.Now.X, Y: minusY))
    {
        retPos.Down = Vec2(X:retPos.Now.X,Y:minusY)
    }
    else{
        retPos.Down = nil
    }

    if(retPos.Up == Vec2() &&
        (maze[plusY][retPos.Now.X] != checkType.rawValue) &&
       beforPos != Vec2(X: retPos.Now.X, Y: plusY))
    {
        retPos.Up = Vec2(X:retPos.Now.X,Y:plusY)
    }else{
        retPos.Up = nil
    }

    if(retPos.Left == Vec2() &&
        (maze[retPos.Now.Y][minusX] != checkType.rawValue) &&
        beforPos != Vec2(X: minusX, Y: retPos.Now.Y))
    {
        retPos.Left = Vec2(X:minusX,Y:retPos.Now.Y)
    }else{
        retPos.Left = nil
    }

    if(retPos.Right == Vec2() &&
        (maze[retPos.Now.Y][plusX] != checkType.rawValue) &&
        beforPos != Vec2(X: plusX, Y: retPos.Now.Y))
    {
        retPos.Right = Vec2(X:plusX,Y:retPos.Now.Y)
    }else{
        retPos.Right = nil
    }


    return retPos
}

// 指定したターゲットの位置を返す
// 見つからなかった場合は、nilが返えってくる
func serchTargetPoint(maze:[[String]],targetMapType:MapType)->Vec2?
{
    var retPos:Vec2? = nil

    let mazeYCount = maze.count - 1
    let mazeXCount = maze[0].count - 1

    for Y in 0...mazeYCount
    {
        for X in 0...mazeXCount{
            let checkValue = maze[Y][X]

            if(checkValue == targetMapType.rawValue)
            {
                retPos = Vec2(X:X,Y:Y)
            }
        }
    }

    return retPos
}

func printMaze(maze:[[String]]){

    let mazeYCount = maze.count - 1
    let mazeXCount = maze[0].count - 1

    for Y in 0...mazeYCount
    {
        print("\n")
        for X in 0...mazeXCount{
            print(maze[Y][X], terminator: "")
        }
    }

    print("\n")
}


printMaze(maze:targetMaze)

let SPos = serchTargetPoint(maze:targetMaze,targetMapType:MapType.Start)
let GPos = serchTargetPoint(maze:targetMaze,targetMapType:MapType.Goal)

print(SPos ?? "スタートなし")
print(GPos ?? "ゴールなし")


let mazeYCount = targetMaze.count - 1
let mazeXCount = targetMaze[0].count - 1

let maxPos = Vec2(X: mazeYCount, Y: mazeXCount)

var RootList:Array<Direction> = Array<Direction>()
RootList.append (CheckRoad(maze:targetMaze,pos: SPos,beforPos: Vec2(X: 0,Y: 0),maxPos: maxPos,checkType: MapType.Wall)!)


var BlackList:Array<Vec2> = Array<Vec2>()

while true {

    let direction = CheckRoad(maze:targetMaze,pos: RootList.last?.Up ?? nil,beforPos: RootList.last?.Now ?? Vec2(),maxPos: maxPos,checkType: MapType.Wall)

    var checkFlag:Bool = false

    for black in BlackList
    {
        if(black == direction?.Now ?? Vec2())
        {
            checkFlag = true
        }
    }

    if(GPos == direction?.Now ?? Vec2())
    {
        break
    }


    if(direction != nil && !checkFlag)
    {
        RootList.append(direction!)
    }else
    {
        let direction = CheckRoad(maze:targetMaze,pos: RootList.last?.Right ?? nil,beforPos: RootList.last?.Now ?? Vec2(),maxPos: maxPos,checkType: MapType.Wall)

        var checkFlag:Bool = false

        for black in BlackList
        {
            if(black == direction?.Now ?? Vec2())
            {
                checkFlag = true
            }
        }

        if(GPos == direction?.Now ?? Vec2())
        {
            break
        }


        if(direction != nil && !checkFlag)
        {
            RootList.append(direction!)
        }else
        {
            let direction = CheckRoad(maze:targetMaze,pos: RootList.last?.Down ?? nil,beforPos: RootList.last?.Now ?? Vec2(),maxPos: maxPos,checkType: MapType.Wall)

            var checkFlag:Bool = false

            for black in BlackList
            {
                if(black == direction?.Now ?? Vec2())
                {
                    checkFlag = true
                }
            }

            if(GPos == direction?.Now ?? Vec2())
            {
                break
            }


            if(direction != nil && !checkFlag)
            {
                RootList.append(direction!)
            }else
            {
                let direction = CheckRoad(maze:targetMaze,pos: RootList.last?.Left ?? nil,beforPos: RootList.last?.Now ?? Vec2(),maxPos: maxPos,checkType: MapType.Wall)

                var checkFlag:Bool = false

                for black in BlackList
                {
                    if(black == direction?.Now ?? Vec2())
                    {
                        checkFlag = true
                    }
                }

                if(GPos == direction?.Now ?? Vec2())
                {
                    break
                }

                if(direction != nil && !checkFlag)
                {
                    RootList.append(direction!)
                }else
                {
                    BlackList.append(RootList.last?.Now ?? Vec2())
                    if(RootList.count > 0)
                    {
                        RootList.removeLast()
                    }else
                    {
                        break
                    }
                }
            }
        }
    }
}

for root in RootList
{
    print(root.Now)
    targetMaze[root.Now.Y][root.Now.X] = MapType.Root.rawValue
}

printMaze(maze:targetMaze)
```

## 感想
- `Enum`のコードに値をセットできるので、コードが読みやすい
- ちょこちょこ出てくる制約に最初はイライラするが、書いているとなれる
- 制約があるおかげで、コードに統一感が出る


