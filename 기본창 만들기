import sys
from PyQt6.QtWidgets import QApplication, QMainWindow, QTextEdit

class Notepad(QMainWindow):
    """
    PyQt6를 사용한 기본 메모장 창 클래스
    """
    def __init__(self):
        """
        생성자 메서드. 부모 클래스의 생성자를 호출하고 UI를 초기화합니다.
        """
        super().__init__()
        self.initUI()

    def initUI(self):
        """
        사용자 인터페이스(UI)를 초기화하는 메서드
        """
        # 텍스트 편집 위젯을 생성합니다.
        self.text_edit = QTextEdit()
        # 이 텍스트 편집 위젯을 창의 중앙 위젯으로 설정합니다.
        self.setCentralWidget(self.text_edit)

        # 창의 제목을 '메모장'으로 설정합니다.
        self.setWindowTitle('메모장')
        
        # 창의 위치와 크기를 설정합니다. (x, y, 너비, 높이)
        self.setGeometry(300, 300, 600, 500)
        
        # 창을 화면에 보여줍니다.
        self.show()

if __name__ == '__main__':
    # QApplication: 프로그램을 실행하고 이벤트 루프를 관리하는 클래스
    app = QApplication(sys.argv)
    
    # 우리가 만든 Notepad 클래스의 인스턴스를 생성합니다.
    notepad = Notepad()
    
    # 프로그램을 실행하고, 창을 닫을 때 프로세스가 종료되도록 합니다.
    sys.exit(app.exec())
