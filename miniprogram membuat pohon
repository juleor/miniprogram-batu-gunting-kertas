/*
 * GLUT Shapes Demo
 *
 * Written by Nigel Stewart November 2003
 *
 * This program is test harness for the sphere, cone
 * and torus shapes in GLUT.
 *
 * Spinning wireframe and smooth shaded shapes are
 * displayed until the ESC or q key is pressed.  The
 * number of geometry stacks and slices can be adjusted
 * using the + and - keys.
 */
#include<windows.h>
#ifdef __APPLE__
#include <GLUT/glut.h>
#else
#include <GL/glut.h>
#include<GL/glu.h>
#endif

#include <stdlib.h>

int flag=1;
GLfloat angle,angle2;
int moving,startx,starty;

/* GLUT callback Handlers */

static void resize(int width, int height)
{
    const float ar = (float) width / (float) height;

    glViewport(0, 0, width, height);
    glMatrixMode(GL_PROJECTION);
    glLoadIdentity();
    glOrtho(-15.0, 15.0, -1.0, 20.0, -15.0, 15.0);

    glMatrixMode(GL_MODELVIEW);
    glLoadIdentity() ;
}
void makecylinder(float height,float Base)
        {
            GLUquadricObj *qobj;
            qobj = gluNewQuadric();
            glColor3f(0.64f, 0.16f, 0.16f);
            glPushMatrix();
            glRotatef(-90, 1.0f, 0.0f, 0.0f);
            gluCylinder(qobj, Base, Base - (0.2 * Base), height, 20, 20);
            glPopMatrix();
        }
void maketree(float height,float Base)
        {

            glPushMatrix();



            float angle;
            makecylinder(height, Base);
            glTranslatef(0.0f, height,0.0f);
            height -=height*0.2f;
            Base -=Base*0.3f;
            for(int a=0; a<3; a++)
            {


                angle = 20+((rand()%50));
                if(angle >48)
                angle = -(20+((rand()%50)));
                if (height > 1)
                {
                    glPushMatrix();
                    if (flag)
                        glRotatef(angle, 1.0f, 0.0f, 1.0f);
                    else
                        glRotatef(angle, 0.0f, 1.0f, 1.0f);
                    flag = !flag;
                    maketree(height, Base); //recursive call
                    glPopMatrix();

                }
                else
                {
                    glColor3f(0.0f, 1.0f / a, 0.0f);
                    glutSolidSphere(0.1f, 10, 10);// for fruits.

                }
            }
            //Glut.glutSwapBuffers();
            glPopMatrix();
        }
static void display(void)
{
    const double t = glutGet(GLUT_ELAPSED_TIME) / 1000.0;
    const double a = t*90.0;
    srand(GLUT_ELAPSED_TIME);
    glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
    glLoadIdentity();
 glRotatef(angle,0,1,0);
 glRotatef(angle2,0,0,1);

    maketree(4.0f,0.1f);
    glutSwapBuffers();
  glFlush();
}


static void key(unsigned char key, int x, int y)
{
    switch (key)
    {
        case 27 :
        case 'q':
            exit(0);
            break;


    }

    glutPostRedisplay();
}



void mouse(int btn,int state,int x,int y)
{
 if(btn==GLUT_LEFT_BUTTON&&state==GLUT_DOWN)
 {
  moving=1;
  startx=x;
  starty=y;
 }
 if(btn==GLUT_LEFT_BUTTON&&state==GLUT_UP)
 {
  moving=0;
 }
}
void motion(int x,int y)
{
 if(moving)
 {
  angle=angle+(x-startx);
  angle2=angle2+(y-starty);
  startx=x;
  starty=y;
  glutPostRedisplay();
 }
}


/* Program entry point */

int main(int argc, char *argv[])
{
    glutInit(&argc, argv);
    glutInitWindowSize(640,480);
    glutInitWindowPosition(10,10);
    glutInitDisplayMode(GLUT_RGB | GLUT_DOUBLE | GLUT_DEPTH);

    glutCreateWindow("Pohon Desain");

    glutReshapeFunc(resize);
    glutDisplayFunc(display);
    glutKeyboardFunc(key);

   glutMouseFunc(mouse);
    glutMotionFunc(motion);

    glClearColor(1,1,1,1);


    glEnable(GL_DEPTH_TEST);


    glutMainLoop();

    return EXIT_SUCCESS;
}
