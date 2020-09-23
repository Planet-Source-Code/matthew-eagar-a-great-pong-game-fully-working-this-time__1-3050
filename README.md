<div align="center">

## A great pong game, fully working this time\!\!


</div>

### Description

This is a fully working pong game, almost identical to the origional one. It has a fairly good (but very basic) computer player, and the ball deflects at different angles depending on how far away from the center of the paddle it is.

I just reposted this, so the code is posted instead of a zip file, that way every body can view it.
 
### More Info
 
'1: Create a new project, and shape form1 so it's width is longer then its height

'2: Add a timer, named timer1, with an interval of 1

'3: add 5 shapes, named shpWallTop, shpWallBottom, shpBall, shpPlayer1 and shpPlayer2

'4: make shpWallTop and shpWallBottom's width the same as the form's width

'5: make shpWallTop and shpWallBottom as wide as the form, with a height of about 300

'6: put shpWallTop at the top of the form, and shpWallBottom at the bottom

'7: Make shpBall a square with a width of 255

'8: make shpPlayer1 and shpPlayer2 's height about 900, and width about 255

'9: place shpPlayer1 about 1 cm from the left side of the form, and shpPlayer2 about 1 cm from the right side.

'10: Paist the following code into the project:


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Matthew Eagar](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/matthew-eagar.md)
**Level**          |Unknown
**User Rating**    |3.0 (9 globes from 3 users)
**Compatibility**  |VB 4\.0 \(16\-bit\), VB 4\.0 \(32\-bit\), VB 5\.0, VB 6\.0
**Category**       |[Games](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/games__1-38.md)
**World**          |[Visual Basic](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/visual-basic.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/matthew-eagar-a-great-pong-game-fully-working-this-time__1-3050/archive/master.zip)





### Source Code

```
Dim vmom As Integer 'vertical momentum
Dim hmom As Integer 'horizontal momentum
Dim padSpeed As Integer 'the speed of the players paddle
Dim origPaddleLoc As Integer
Dim origBallLocY As Integer
Dim origBallLocX As Integer
Private Sub Form_KeyDown(KeyCode As Integer, Shift As Integer)
If KeyCode = 38 Then 'the up key
 padSpeed = -150
ElseIf KeyCode = 40 Then 'the down key
 padSpeed = 150
End If
End Sub
Private Sub Form_KeyUp(KeyCode As Integer, Shift As Integer)
padSpeed = 0 'stop the paddle from moving
End Sub
Private Sub Form_Load()
hmom = -150
vmom = 0
'record the origional starting locations for everything
origPaddleLoc = shpPlayer1.Top
origBallLocX = shpBall.Left
origBallLocY = shpBall.Top
End Sub
Private Sub Timer1_Timer()
'move the ball
shpBall.Top = shpBall.Top + vmom
shpBall.Left = shpBall.Left + hmom
'check to see if the ball's hit a wall
If shpBall.Top + shpBall.Height >= shpWallBottom.Top Then
 shpBall.Top = shpWallBottom.Top - shpBall.Height
 vmom = -vmom
 Beep
ElseIf shpBall.Top <= shpWallTop.Top + shpWallTop.Height Then
 shpBall.Top = shpWallTop.Top + shpWallTop.Height
 vmom = -vmom
 Beep
End If
'move the paddle
If padSpeed <> 0 Then
 shpPlayer1.Top = shpPlayer1.Top + padSpeed
End If
'check to see if the paddle's hit a wall
If shpPlayer1.Top <= shpWallTop.Top + shpWallTop.Height Then
 shpPlayer1.Top = shpWallTop.Top + shpWallTop.Height
ElseIf shpPlayer1.Top + shpPlayer1.Height >= shpWallBottom.Top Then
 shpPlayer1.Top = shpWallBottom.Top - shpPlayer1.Height
End If
If shpPlayer2.Top <= shpWallTop.Top + shpWallTop.Height Then
 shpPlayer2.Top = shpWallTop.Top + shpWallTop.Height
ElseIf shpPlayer2.Top + shpPlayer2.Height >= shpWallBottom.Top Then
 shpPlayer2.Top = shpWallBottom.Top - shpPlayer2.Height
End If
'move the computer player's paddle
If shpBall.Top < shpPlayer2.Top Then
 shpPlayer2.Top = shpPlayer2.Top - 250
ElseIf shpBall.Top > shpPlayer2.Top + shpPlayer2.Height Then
 shpPlayer2.Top = shpPlayer2.Top + 250
End If
'if the ball has hit player 1's paddle
If shpBall.Left <= shpPlayer1.Left + shpPlayer1.Width And shpBall.Left >= shpPlayer1.Left - shpPlayer1.Width Then
 If shpBall.Top + shpBall.Height >= shpPlayer1.Top And shpBall.Top <= shpPlayer1.Top + shpPlayer1.Height Then
 'calculate the angle it's deflecting off at
 tmp = ((shpPlayer1.Top + (shpPlayer1.Height / 2)) - (shpBall.Top + (shpBall.Height / 2))) * 0.55
 vmom = vmom + -tmp
 Beep
 shpBall.Left = shpPlayer1.Left + shpPlayer1.Width
 'deflect the ball
 hmom = -hmom
 End If
End If
'if the ball has hit player 2's paddle
If shpBall.Left + shpBall.Width >= shpPlayer2.Left And shpBall.Left <= shpPlayer2.Left + shpPlayer2.Width Then
 If shpBall.Top + shpBall.Height >= shpPlayer2.Top And shpBall.Top <= shpPlayer2.Top + shpPlayer2.Height Then
 'calculate the angle it's deflecting off at
 tmp = ((shpPlayer2.Top + (shpPlayer2.Height / 2)) - (shpBall.Top + (shpBall.Height / 2))) * 0.55
 vmom = vmom + -tmp
 Beep
 shpBall.Left = shpPlayer2.Left - shpBall.Width
 'deflect the ball
 hmom = -hmom
 End If
End If
'see if someone's won
If shpBall.Left + shpBall.Width < 0 Then
 'reset the ball and paddles to their origional location
 shpBall.Left = origBallLocX
 shpBall.Top = origBallLocY
 shpPlayer1.Top = origPaddleLoc
 shpPlayer2.Top = origPaddleLoc
 hmom = -150
 vmom = 0
ElseIf shpBall.Left > Form1.Width Then
 'reset the ball and paddles to their origional location
 shpBall.Left = origBallLocX
 shpBall.Top = origBallLocY
 shpPlayer1.Top = origPaddleLoc
 shpPlayer2.Top = origPaddleLoc
 hmom = 150
 vmom = 0
End If
End Sub
```

