// Tieling Chen, April, 2020
#include "../myObjects2020.cpp"


//------ global variables and constants------------
GLsizei ww = 512;
GLsizei wh = 512;
GLfloat left, right, bottom, top, near = 5, far = 20;
const float REGION_DIM = 4;
GLfloat theta = 30, phi = 60, rho = 10;
GLfloat dTheta = 5, dPhi = 5, dRho = 0.5;
GLfloat alpha = 0, beta = 0, gama = 0;
GLfloat dAlpha = 5, dBeta = 5, dGama = 5;
GLfloat a = 1, b = 1, c = 1, d = 1;
GLfloat dA = 0.1, dB = 0.1, dC = 0.1, dD = 0.01;
GLfloat direction = 1.0;
GLfloat lightPosition[4] = { 2, 1, 3, 1 };
GLfloat lightAmbient[4] = { 0.0, 0.0, 0.0, 1.0 };
GLfloat lightDiffuse[4] = { 1.0, 1.0, 1.0, 1.0 };
GLfloat lightSpecular[4] = { 1.0, 1.0, 1.0, 1.0 };
GLfloat materialAmbient[4] = { 0.33, 0.22, 0.03, 1.0 };
GLfloat materialDiffuse[4] = { 0.78, 0.57, 0.11, 1.0 };
GLfloat materialSpecular[4] = { 0.99, 0.91, 0.81, 1.0 };
GLfloat materialShininess = 27.8;
GLfloat R2 = 2 * b;
GLUquadric* qobj;
//----- prototypes ----------
void display(void);
void init(void);
void reshape(GLsizei w, GLsizei h);
void keys(unsigned char k, int x, int y);
void mouse(int, int, int, int);
void idle(void);
void wheel();
void ball();
void blade();

void hyperboloidOneN(float a, float b, float c, int slices, int stacks)
{
	float z1, z2;
	float dz = 2.0 * c / stacks;
	int dTheta = (int)(360.0 / slices);
	float p1[3], p2[3], p3[3], p4[3];
	float n1[3], n2[3], n3[3], n4[4];
	float xAxis1, yAxis1, xAxis2, yAxis2;

	for (int i = 0; i < stacks; i++)
	{
		for (int theta = 0; theta <= 360; theta += dTheta)
		{
			z1 = -1.0 * c + i * dz;
			xAxis1 = a * sqrt(1 + (z1 / c) * (z1 / c));
			yAxis1 = b * sqrt(1 + (z1 / c) * (z1 / c));

			z2 = z1 + dz;
			xAxis2 = a * sqrt(1 + (z2 / c) * (z2 / c));
			yAxis2 = b * sqrt(1 + (z2 / c) * (z2 / c));

			p1[0] = xAxis1 * cos(theta * DtoR);
			p1[1] = yAxis1 * sin(theta * DtoR);
			p1[2] = z1;
			n1[0] = p1[0] / a / a;
			n1[1] = p1[1] / b / b;
			n1[2] = -1.0 * p1[2] / c / c;
			normalize(n1);

			p2[0] = xAxis1 * cos((theta + dTheta) * DtoR);
			p2[1] = yAxis1 * sin((theta + dTheta) * DtoR);
			p2[2] = z1;
			n2[0] = p2[0] / a / a;
			n2[1] = p2[1] / b / b;
			n2[2] = -1.0 * p2[2] / c / c;
			normalize(n2);

			p3[0] = xAxis2 * cos((theta + dTheta) * DtoR);
			p3[1] = yAxis2 * sin((theta + dTheta) * DtoR);
			p3[2] = z2;
			n3[0] = p3[0] / a / a;
			n3[1] = p3[1] / b / b;
			n3[2] = -1.0 * p3[2] / c / c;
			normalize(n3);

			p4[0] = xAxis2 * cos(theta * DtoR);
			p4[1] = yAxis2 * sin(theta * DtoR);
			p4[2] = z2;
			n4[0] = p4[0] / a / a;
			n4[1] = p4[1] / b / b;
			n4[2] = -1.0 * p4[2] / c / c;
			normalize(n4);

			glBegin(GL_POLYGON);
			glNormal3fv(n1);
			glVertex3fv(p1);

			glNormal3fv(n2);
			glVertex3fv(p2);

			glNormal3fv(n3);
			glVertex3fv(p3);

			glNormal3fv(n4);
			glVertex3fv(p4);
			glEnd();
		}
	}
}


void display(void)
{
	glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
	glEnable(GL_DEPTH_TEST);

	glMatrixMode(GL_MODELVIEW);
	glLoadIdentity();
	gluLookAt(rho * sin(theta * DtoR) * sin(phi * DtoR), rho * cos(phi * DtoR), rho * cos(theta * DtoR) * sin(phi * DtoR), 0, 0, 0, 0, 1, 0);

	glDisable(GL_LIGHTING);		// enable lighting
	axes(REGION_DIM);

	glEnable(GL_LIGHTING);		// enable lighting
	glEnable(GL_LIGHT0);
	glLightModeli(GL_LIGHT_MODEL_TWO_SIDE, GL_TRUE);

	glRotatef(alpha, 1, 0, 0);
	glRotatef(beta, 0, 1, 0);
	glRotatef(gama, 0, 0, 1);

	//glRotatef(-90, 1, 0, 0);

	//hyperboloidOneN(a, b, c, 80, 40);
	axes(REGION_DIM);
	
	//----- Ring 1 -----------------
	//glRotatef(alpha, 0, 1, 0); //y, left click
	// Rotate(angle, x cord, y cord, z cord)
	//glRotatef(90, 1, 0, 0);
	
	//glPolygonMode(GL_FRONT_AND_BACK, GL_FILL);
	//glutSolidTorus(0.1 * a, R2, 40, 40);
	//cylinder(.3, 3);
	//glColor3f(0, 1, .8);
	
	wheel();

	//glRotatef(90, 0, 1, 0);
	
	blade();
	/*glColor3f(0, 0, .8);
	glTranslatef(0, 0, 4);
	glPolygonMode(GL_FRONT_AND_BACK, GL_FILL);
	ball();*/
	glutSwapBuffers();
	glutPostRedisplay();	// work with GLUT_DOUBLE
}
void ball()
{
	gluSphere(qobj, .4, 40, 40);
}
void wheel()
{
	glPushMatrix();
	//glColor3f(0, 1, .8);
	glRotatef(-90, 1, 0, 0);
	glTranslatef(-0.2, 0, 0);
	//gluquadratic * quad, base, top, height, slices, stacks
	//gluCylinder(qobj, .3, .3, 2, 80, 80);
	gluCylinder(qobj, .2, .1, 4, 40, 40);
	glPopMatrix();
}
void blade() 
{
	glPushMatrix();
	glTranslatef(0, 0, .2);
	gluCylinder(qobj, .1, .1, 2, 20, 20);
	glPopMatrix();
}
void cleanup()
{
	gluDeleteQuadric(qobj);
}

void init(void)
{
	float ratio = ww * 1.0 / (wh * 1.0);

	qobj = gluNewQuadric();
	gluQuadricNormals(qobj, GLU_SMOOTH);

	glClearColor(0.5, 0.5, 0.5, 1.0);	// background color; default black; (R, G, B, Opacity)
	glColor3f(0.5, 0.9, 1);
	glEnable(GL_LIGHTING);		// enable lighting
	glEnable(GL_LIGHT0);

	glLightfv(GL_LIGHT0, GL_POSITION, lightPosition);
	glLightfv(GL_LIGHT0, GL_AMBIENT, lightAmbient);
	glLightfv(GL_LIGHT0, GL_DIFFUSE, lightDiffuse);
	glLightfv(GL_LIGHT0, GL_SPECULAR, lightSpecular);

	glMaterialfv(GL_FRONT_AND_BACK, GL_AMBIENT, materialAmbient);
	glMaterialfv(GL_FRONT_AND_BACK, GL_DIFFUSE, materialDiffuse);
	glMaterialfv(GL_FRONT_AND_BACK, GL_SPECULAR, materialSpecular);
	glMaterialf(GL_FRONT_AND_BACK, GL_SHININESS, materialShininess);

	glMatrixMode(GL_PROJECTION);
	glLoadIdentity();
	if (ratio >= 1)
	{
		left = -1.0 * REGION_DIM * ratio;
		right = REGION_DIM * ratio;
		bottom = -1.0 * REGION_DIM;
		top = REGION_DIM;
	}
	else
	{
		left = -1.0 * REGION_DIM;
		right = REGION_DIM;
		bottom = -1.0 * REGION_DIM / ratio;
		top = REGION_DIM / ratio;
	}

	glFrustum(left, right, bottom, top, near, far);

	glMatrixMode(GL_MODELVIEW);
}

void reshape(GLsizei w, GLsizei h)
{
	float ratio = w * 1.0 / (h * 1.0);

	glMatrixMode(GL_PROJECTION);
	glLoadIdentity();
	if (ratio >= 1)
	{
		left = -1.0 * REGION_DIM * ratio;
		right = REGION_DIM * ratio;
		bottom = -1.0 * REGION_DIM;
		top = REGION_DIM;
	}
	else
	{
		left = -1.0 * REGION_DIM;
		right = REGION_DIM;
		bottom = -1.0 * REGION_DIM / ratio;
		top = REGION_DIM / ratio;
	}

	glFrustum(left, right, bottom, top, near, far);

	glMatrixMode(GL_MODELVIEW);
	glViewport(0, 0, w, h);

	//------ reset the window size
	ww = w;
	wh = h;
}

void idle()
{
	alpha += 0.1;
	beta += 0.1;
	gama += 0.1;

	if (alpha >= 360)
		alpha -= 360;

	if (beta >= 360)
		beta -= 360;

	if (gama >= 360)
		gama -= 360;

	glutPostRedisplay();
}


void mouse(int button, int state, int x, int y)
{
	if (button == GLUT_LEFT_BUTTON && state == GLUT_DOWN)
	{
		alpha += dAlpha * direction;
	}
	else if (button == GLUT_MIDDLE_BUTTON && state == GLUT_DOWN)
	{
		beta += dBeta * direction;
	}
	else if (button == GLUT_RIGHT_BUTTON && state == GLUT_DOWN)
	{
		gama += dGama * direction;
	}
}

void keys(unsigned char k, int x, int y)
{
	if (k == 'p' || k == 'P')
		direction = 1.0;
	else if (k == 'n' || k == 'N')
		direction = -1.0;
	else if (k == 'a' || k == 'A')
		a += dA * direction;
	else if (k == 'b' || k == 'B')
		b += dB * direction;
	else if (k == 'c' || k == 'C')
		c += dC * direction;
	else if (k == 'd' || k == 'D')
		d += dD * direction;
	else if (k == 'i' || k == 'I')
		glutIdleFunc(idle);
	else if (k == 'q' || k == 'Q')
		glutIdleFunc(NULL);
	else if (k == '+')
		rho -= dRho;
	else if (k == '-')
		rho += dRho;
	else if (k == 'r' || k == 'R')
	{
		near = 5;
		far = 20;
		theta = 30;
		phi = 60;
		rho = 10;
		alpha = 0;
		beta = 0;
		gama = 0;
		a = 1;
		b = 1;
		c = 1;
		d = 1;
		direction = 1.0;
		glutIdleFunc(NULL);
	}
}
void specialKeys(int k, int x, int y)
{
	if (k == GLUT_KEY_LEFT)
		theta -= dTheta;
	else if (k == GLUT_KEY_RIGHT)
		theta += dTheta;
	else if (k == GLUT_KEY_UP)
	{
		if (phi > dPhi)
			phi -= dPhi;
		else if (phi == dPhi)
			phi = 0.01;		// to keep the direction vector of the camera
	}
	else if (k == GLUT_KEY_DOWN)
	{
		if (phi <= 180 - dPhi)
			phi += dPhi;
	}
}

int main()
{
	glutInitDisplayMode(GLUT_DOUBLE | GLUT_RGB); // GLUT_DOUBLE work with glutPostRedisplay
	glutInitWindowSize(ww, wh);	// default size 300 by 300
	glutInitWindowPosition(100, 100); // defualt at (0, 0)
	glutCreateWindow("Shea Moore");
	init();

	glutDisplayFunc(display);
	glutReshapeFunc(reshape);
	glutMouseFunc(mouse);
	glutKeyboardFunc(keys);
	glutSpecialFunc(specialKeys);
	//glutIdleFunc(idle);

	glutMainLoop();
	return 1;
}
