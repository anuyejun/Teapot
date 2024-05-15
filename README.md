#include <GL/glut.h>

float angleY = 0.0; // Y축 회전 각도를 저장하는 변수
float angleX = 0.0; // X축 회전 각도를 저장하는 변수

// 초기화 함수
void initOpenGL() {
    glEnable(GL_DEPTH_TEST); // 깊이 테스트 활성화
    glClearColor(0.0, 0.0, 0.0, 1.0); // 배경색을 검정색으로 설정
}

// 디스플레이 콜백 함수
void display() {
    glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT); // 화면과 깊이 버퍼 클리어
    glLoadIdentity(); // 변환 행렬을 단위 행렬로 초기화
    
    
    glRotatef(angleX, 1.0, 0.0, 0.0); // X축을 중심으로 회전
    glRotatef(angleY, 0.0, 1.0, 0.0); // Y축을 중심으로 회전
    
    // 주전자를 그림
    glColor3f(1.0, 0.5, 0.5); // 주전자의 색을 붉은색 계열로 설정
    glutWireTeapot(0.5); // 와이어 프레임 모드로 주전자를 그림
    
    glutSwapBuffers(); // 프론트 버퍼와 백 버퍼를 교환
}

// 타이머 콜백 함수
void timer(int value) {
    angleY += 2.0; // Y축 각도를 2도 씩 증가
    angleX += 1.0; // X축 각도를 1도 씩 증가
    if (angleY > 360) {
        angleY -= 360;
    }
    if (angleX > 360) {
        angleX -= 360;
    }
    
    glutPostRedisplay(); // 디스플레이 콜백 함수를 호출하여 화면을 다시 그림
    glutTimerFunc(16, timer, 0); // 다음 타이머 이벤트를 16ms 후에 설정
}

int main(int argc, char** argv) {
    glutInit(&argc, argv); // GLUT를 초기화
    glutInitDisplayMode(GLUT_DOUBLE | GLUT_RGB | GLUT_DEPTH); // 디스플레이 모드 설정
    glutInitWindowSize(500, 500); // 윈도우 크기 설정
    glutInitWindowPosition(100, 100); // 윈도우 위치 설정
    glutCreateWindow("OpenGL 회전 주전자 예제"); // 윈도우 생성
    
    initOpenGL(); // OpenGL 초기화 함수 호출
    
    glutDisplayFunc(display); // 디스플레이 콜백 함수 등록
    glutTimerFunc(0, timer, 0); // 타이머 콜백 함수 등록
    
    glutMainLoop(); // 이벤트 처리 루프 진입
    
    return 0;
}
