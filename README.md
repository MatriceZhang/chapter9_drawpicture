chapter9_drawpicture
====================


//
//  main.cpp
//  chapter9_inherience
//
//  Created by zhangshiyu on 11/17/14.
//  Copyright (c) 2014 ZSY. All rights reserved.
//

#include <iostream>
#include "msoftcon.h"    //for graphic function
class shape
{
protected:
    int xCo,yCo;    //coordinates of shape
    color fillcolor;  //clor
    fstyle fillstyle;   //fill pattern
public:
    shape():xCo(0),yCo(0),fillcolor(cWHITE),fillstyle(SOLID_FILL)
    { }   //4_arg constructor
    shape(int x, int y, color fc,fstyle fs):
    xCo(x),yCo(y),fillcolor(fc),fillstyle(fs)
    { }
    void draw() const  //set color and fill style
    {
    set_color(fillcolor);
    set_fill_style(fillstyle);
}
};

class circle:public shape
{
private:
    int radius;
public:
    circle():shape()
    {}
    circle(int x, int y,int r, color fc,fstyle fs)
    :shape(x,y,fc,fs),radius(r)      //5-arg constuctor
    { }
    void draw() const   //draw the cicle
    {
        shape::draw();
        draw_circle(xCo, yCo, radius);
    }
};

/////////////////
class rect:public shape
{
private:
    int width,height;   //(xCo,yCo)is upper-left cornor
public:
    rect():shape(),height(0),width(0)   //no-arg constructor
    {}
    rect(int x,int y, int h,int w,color fc,fstyle fs):
    shape(x,y,fc,fs),height(h),width(w)
    {}
    void draw() const   //draw the rectangle
    {
        shape::draw();
        draw_rectangle(xCo, yCo, xCo+width, yCo+height);
        set_color(cWHITE);   //draw diagonal
        draw_line(xCo,yCo,xCo+width,yCo+height);
    }
};

////
class tria:public shape
{
private:
    int height;   //(xCo,yCo) is tip of pyramid
public:
    tria():shape(),height(0)
    {}
    tria(int x,int y, int h, color fc,fstyle fs):
    shape(x,y,fc,fs),height(h)
    {}
    void draw() const
    {
        shape::draw();
        draw_pyramid(xCo, yCo, height);
    }
};
///////////////
int main()
{
    init_graphics();   //initualize graphics system
    
    circle cir(40,12,5,cBLUE,X_FILL);        //create circle
    rect rec(12,7,10,15,cRED,SOLID_FILL);     //create rectangle
    tria tri(60,7,11,cGREEN,MEDIUM_FILL);   //create triangle
    cir.draw();//draw circle
    rec.draw();
    tri.draw();
    set_cursor_pos(1, 25);
    return 0;
}




