---
layout: post
title:  "[MFC] 消息和事件"
date:   2016-07-24 00:00:23 +0800
categories: [mfc]
author: Jimmy Sue
---

## 消息映射表

1. 在类中进行申明：

``` c++
#include <afxwin.h>

class CSimpleFrame: public CFrameWnd
{
public:
    CSimpleFrame();
protected:
    afx_msg int OnCreate(LPCREATESTRUCT lpCreateStruct);
    /* 
    macro should be provided at the end of the class
    actual message should be listed just above declare macro
    */
    DECLARE_MESSAGE_MAP()
}
```

2. 创建消息映射表以实现消息

``` c++
BEGIN_MESSAGE_MAP(CSimpleFrame, CFrameWnd)
    ON_WM_CREATE() // 要实现的消息, 类中对应成员函数 OnCreate(...)
END_MESSAGE_MAP
```

## Windows Messages

 - WM_CREATE
 - WM_SHOWWINDOW
 - WM_ACTIVATION
 - WM_PAINT
 - WM_SIZING
 - WM_MOVE
 - WM_DESTROY

## Command Messages

### Creating a Command Message

    associate a member function to a command message

``` c++
ON_COMMAND(IDentifier, MethodName)
```

IDentifier must be the identifier of the menu item or Window control
MethodName member function implement the action of menu item or window control

## Keyboard Message

| Virtual Key | Used for |
|-------------|----------|
| VK_F1 | F1|
| VK_F2 | F2 |
| VK_F... | F...|
| VK_F11 | F11 |
| VK_SCROLL | Scroll Lock|
| ... | ...|

### Practical Learning
``` c++
BEGIN_MESSAGE_MAP(CMainFrame, CFrameWnd)
    ON_WM_CREATE()
    ON_WM_KEYDOWN()
END_MESSAGE_MAP()
```

``` c++
void CMainFrame::OnKeyDown(UINT nChar, UINT nRepCnt, UINT nFlags)
{
    switch(nChar)
    {
    case VK_RETURN:
        MessageBox("You pressed Enter");
        break;
    case VK_F1:
        MessageBox("Help is not available at the moment");
        break;  
    case VK_DELETE:
        MessageBox("Can't Delete This");
        break;
    default:
        MessageBox("Whatever");
    }
}
```


## Mouse Mesage

### left mouse button was pressed

If the left mouse button was pressed, an ON_WM_LBUTTONDOWN message is sent.
The syntax of this message is:

    afx_msg void OnLButtonDown(UINT nFlags, CPoint point);

The first argument, nFlags, specifies what button is down or what keyboard key and what
mouse button are down. It is a constant integer that can have one of the following values:
|Value | Description |
|------|-------------|
|MK_CONTROL|A Ctrl key is held down         |
|MK_LBUTTON|The left mouse button is down   |
|MK_MBUTTON|The middle mouse button is down |
|MK_RBUTTON|The right mouse button is down  |
|MK_SHIFT  |A Shift key is held down        |

### left mouse **is being** released

If the left mouse is being released, the ON_WM_LBUTTONUP message is sent. Its
syntax is:

    afx_msg void OnLButtonUp(UINT nFlags, CPoint point);

The first argument, nFlags, specifies what button, right or middle, is down or what
keyboard key and what mouse button were down. It is a constant integer that can have
one of the following values:
|Value       |Description                       |
|------------|----------------------------------|
|MK_CONTROL  |A Ctrl key was held down          |
|MK_MBUTTON  |The middle mouse button was down  |
|MK_RBUTTON  |The right mouse button was down   |
|MK_SHIFT    |A Shift key was held              |

### mouse move

After pressing one of the mouse buttons, depending on the requirement, the use may not
need to immediately release the button. Another action performed with the mouse
consists of clicking and holding the mouse button down, then dragging in a chosen
direction. This action refers to the mouse moving. When this is done a
WM_MOUSEMOVE message is sent. Its syntax is:

    afx_msg void OnMouseMove(UINT nFlags, CPoint point);
    
The nFlags argument specifies what button is held down or what key is pressed in
combination with the button that is held down while the mouse pointer is moving. This
argument can have one of the following values:

|Value       |While the mouse is moving|
|------------|--------------------------|
|MK_CONTROL  |A Ctrl key is held down           |
|MK_LBUTTON  |The left mouse button is down|
|MK_MBUTTON  |The middle mouse button is down|
|MK_RBUTTON  |The right mouse button is down|
|MK_SHIFT    |A Shift key was held down|

The point argument specifies the current location of the mouse pointer in x (horizontal)
and y (vertical) coordinates at the time the message is captured.


## Anytime Message

two versions of SendMessage():

``` c++
    //The Win32 API version of the SendMessage() function has the following syntax:
    LRESULT SendMessage(HWND hWnd, UINT Msg, WPARAM wParam, LPARAM lParam);
    //The MFC version is carried by the CWnd class and declared as follows:
    LRESULT SendMessage(UINT Msg, WPARAM wParam, LPARAM lParam);
```   

## Reference

1. Visual C++ and MFC programing, 2nd Edition
