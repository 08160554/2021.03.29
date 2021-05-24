#2021.03.29
WEEK06

01
----------
```C

#include <GL/glut.h>
#include <stdio.h>
float vx[2000],vy[2000];  ///準備一個頂點
int N=0;        ///有N個頂點
float angle=0;
void display()
{
    glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
    glPushMatrix();    ///備份矩陣
        glRotatef(angle,0,0,1);   ///旋轉，對Z軸轉
        glScalef(0.5,0.1,0.1);    ///調成細長的
        glColor3f(0.3,0.3,1.0);    ///藍色
        glutSolidCube(1);    ///方塊

    glPopMatrix();
    glutSwapBuffers();
}
void motion (int x,int y)
{
    angle++;       ///只要mouse在motion時，就會增加角度
    display();    ///增加後，重畫畫面
}
void keyboard(unsigned char key,int x,int y)
{

}
int main(int argc,char ** argv)
{
    glutInit(&argc,argv);
    glutInitDisplayMode(GLUT_DOUBLE | GLUT_DEPTH);
    glutCreateWindow("08160554");
    glutDisplayFunc(display);
   // glutKeyboardFunc(keyboard);      ///按下去彈起來
    glutMotionFunc(motion);    ///mouse motion 在動
    glutMainLoop();
}
```
02
----------

```c
#include <GL/glut.h>
float angle=0;
void display()
{
    glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
    glPushMatrix();
        glRotatef(angle++,0,0,1);   ///要轉動angle
        glutSolidCube(1);
    glPopMatrix();
    glutSwapBuffers();
}

int main(int argc,char ** argv)
{
    glutInit(&argc,argv);
    glutInitDisplayMode(GLUT_DOUBLE | GLUT_DEPTH);
    glutCreateWindow("08160554");
    glutDisplayFunc(display); 
    glutIdleFunc(display);   ///idle很閒的時候，就重畫
    glutMainLoop();
}
```

03
----------
```c
#include <GL/glut.h>
float angle=0;
void display()
{
    glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
    glPushMatrix();
        ///glTranslatef(0,0,0);    ///把正確轉動的手臂掛在肩上
        ///glRotatef(angle++,0,0,1);  ///轉動
        glTranslatef(-0.25,0,0);   ///將旋轉中心放在正中心
        glScalef(0.5,0.1,0.1);   ///細細長長的
        glutSolidCube(1);   ///方塊
    glPopMatrix();
    glutSwapBuffers();
}

int main(int argc,char ** argv)
{
    glutInit(&argc,argv);
    glutInitDisplayMode(GLUT_DOUBLE | GLUT_DEPTH);
    glutCreateWindow("08160554");
    glutIdleFunc(display);
    glutDisplayFunc(display);
    glutMainLoop();
}
```

04
---------
```c
#include <GL/glut.h>
float angle=0;
void hand()
{
    glPushMatrix();
        glScalef(0.5,0.1,0.1);
        glutSolidCube(1);
    glPopMatrix();
}
void display()
{
    glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
    glPushMatrix();
        glTranslatef(-0.25,0,0);   ///把正確轉動的手臂掛在肩上
        glRotatef(angle++,0,0,1);   ///轉動
        glTranslatef(-0.25,0,0);
        hand();
    glPopMatrix();
    hand();
    glutSwapBuffers();
}

int main(int argc,char ** argv)
{
    glutInit(&argc,argv);
    glutInitDisplayMode(GLUT_DOUBLE | GLUT_DEPTH);
    glutCreateWindow("08160554");
    glutIdleFunc(display);
    glutDisplayFunc(display);
    glutMainLoop();
}
```

05
--------
```c
#include <GL/glut.h>
float angle=0;
void hand()
{
    glPushMatrix();
        glScalef(0.5,0.1,0.1);
        glutSolidCube(1);
    glPopMatrix();
}
void display()
{
    glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
    glPushMatrix();
        glTranslatef(-0.25,0,0);   ///手臂掛上去肩關節
        glRotatef(angle,0,0,1);    ///轉動(這裡沒有++)
        glTranslatef(-0.25,0,0);   ///將旋轉中心放在正中心
        hand();   ///上手臂
        glPushMatrix();
            glTranslatef(-0.25,0,0);   ///把正確轉動的手掛在肩上
            glRotatef(angle,0,0,1);    ///轉動
            glTranslatef(-0.25,0,0);   ///將旋轉中心放在正中心
            hand();   ///下手臂
        glPopMatrix();
    glPopMatrix();
    glutSwapBuffers();
    angle++;   ///要在外面++
}

int main(int argc,char ** argv)
{
    glutInit(&argc,argv);
    glutInitDisplayMode(GLUT_DOUBLE | GLUT_DEPTH);
    glutCreateWindow("08160554");
    glutIdleFunc(display);
    glutDisplayFunc(display);
    glutMainLoop();
}
```

06
--------
```c
#include <GL/glut.h>
float angle=0;
void hand()
{
    glPushMatrix();
        glScalef(0.5,0.1,0.1);
        glutSolidCube(1);
    glPopMatrix();
}
void display()
{
    glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
    glPushMatrix();
        glTranslatef(-0.25,0,0);
        glRotatef(angle,0,0,1);
        glTranslatef(-0.25,0,0);
        hand();
        glPushMatrix();
            glTranslatef(-0.25,0,0);
            glRotatef(angle,0,0,1);
            glTranslatef(-0.25,0,0);
            hand();
        glPopMatrix();
    glPopMatrix();

    glPushMatrix();
        glTranslatef(+0.25,0,0);
        glRotatef(-angle,0,0,1);
        glTranslatef(+0.25,0,0);
        hand();
        glPushMatrix();
            glTranslatef(+0.25,0,0);
            glRotatef(-angle,0,0,1);
            glTranslatef(+0.25,0,0);
            hand();
        glPopMatrix();
    glPopMatrix();

    glutSwapBuffers();
    angle++;
}

int main(int argc,char ** argv)
{
    glutInit(&argc,argv);
    glutInitDisplayMode(GLUT_DOUBLE | GLUT_DEPTH);
    glutCreateWindow("08160554");
    glutIdleFunc(display);
    glutDisplayFunc(display);
    glutMainLoop();
}
```

07-homework
------
```c
#include <GL/glut.h>
#include <math.h>
float angle=0;
void hand()
{
    glPushMatrix();
        glScalef(0.2,0.2,0.2);
        glutSolidCube(1);
    glPopMatrix();
}
void display()
{
    glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
    glColor3f(1,1,1);
    glPushMatrix();
        glTranslatef(-0.2,0,0);
        glRotatef(angle,0,0,1);
        glTranslatef(-0.2,0,0);
        hand();
        glPushMatrix();
            glTranslatef(-0.1,0,0);
            glRotatef(angle,0,0,1);
            glTranslatef(-0.1,0,0);
            hand();

            glTranslatef(-0.11,0,0);
            glRotatef(angle,0,0,1);
            glTranslatef(-0.11,0,0);
            hand();
        glPopMatrix();
    glPopMatrix();

    glPushMatrix();
        glTranslatef(+0.2,0,0);
        glRotatef(angle,0,0,1);
        glTranslatef(+0.2,0,0);
        hand();
        glPushMatrix();
            glTranslatef(+0.1,0,0);
            glRotatef(angle,0,0,1);
            glTranslatef(+0.1,0,0);
            hand();

            glTranslatef(+0.11,0,0);
            glRotatef(angle,0,0,1);
            glTranslatef(+0.11,0,0);
            hand();
        glPopMatrix();
    glPopMatrix();

    glColor3f(0,1,1);
    glBegin(GL_POLYGON);
        glVertex3f( 0.3, 0.2,-0.6);
        glVertex3f( 0.3,-0.9,-0.6);
        glVertex3f(-0.3,-0.9,-0.6);
        glVertex3f(-0.3, 0.2,-0.6);

    glEnd();
    glColor3f(0,1,1);
    glBegin(GL_POLYGON);
        glVertex3f( 0.2, 0.5,-0.6);
        glVertex3f( 0.2,-0.2,-0.6);
        glVertex3f(-0.2,-0.2,-0.6);
        glVertex3f(-0.2, 0.5,-0.6);
    glEnd();

    glColor3f(0,0,0);
    glBegin(GL_POLYGON);
        glVertex3f( -0.05, 0.3,-0.2);
        glVertex3f(-0.05,0.4,-0.2);
        glVertex3f(-0.15,0.4,-0.2);
        glVertex3f(-0.15, 0.3,-0.2);
    glEnd();
    glColor3f(0,0,0);
    glBegin(GL_POLYGON);
        glVertex3f( +0.05, 0.3,-0.2);
        glVertex3f(+0.05,0.4,-0.2);
        glVertex3f(+0.15,0.4,-0.2);
        glVertex3f(+0.15, 0.3,-0.2);
    glEnd();

    glutSwapBuffers();
    angle++;
}

int main(int argc,char ** argv)
{
    glutInit(&argc,argv);
    glutInitDisplayMode(GLUT_DOUBLE | GLUT_DEPTH);
    glutCreateWindow("08160554");
    glutIdleFunc(display);
    glutDisplayFunc(display);
    glutMainLoop();
}

```
