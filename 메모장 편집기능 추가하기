import sys
from PyQt6.QtWidgets import QApplication, QMainWindow, QTextEdit, QFileDialog
from PyQt6.QtGui import QAction

class Notepad(QMainWindow):
    """
    PyQt6를 사용한 기본 메모장 창 클래스
    """
    def __init__(self):
        """
        생성자 메서드. 부모 클래스의 생성자를 호출하고 UI를 초기화합니다.
        """
        super().__init__()
        # 현재 열려있는 파일 경로를 저장하기 위한 변수
        self.current_file = None
        self.initUI()

    def initUI(self):
        """
        사용자 인터페이스(UI)를 초기화하는 메서드
        """
        # 텍스트 편집 위젯을 생성합니다.
        self.text_edit = QTextEdit()
        # 이 텍스트 편집 위젯을 창의 중앙 위젯으로 설정합니다.
        self.setCentralWidget(self.text_edit)

        # 메뉴바 생성
        menubar = self.menuBar()
        file_menu = menubar.addMenu('파일(&F)') # '&F'는 Alt+F 단축키를 의미

        # '새로만들기' 액션
        new_action = QAction('새로만들기', self)
        new_action.setShortcut('Ctrl+N')
        new_action.triggered.connect(self.new_file)

        # '열기' 액션
        open_action = QAction('열기', self)
        open_action.setShortcut('Ctrl+O')
        open_action.triggered.connect(self.open_file)

        # '저장' 액션
        save_action = QAction('저장', self)
        save_action.setShortcut('Ctrl+S')
        save_action.triggered.connect(self.save_file)

        # '다른 이름으로 저장' 액션
        save_as_action = QAction('다른 이름으로 저장', self)
        save_as_action.triggered.connect(self.save_as_file)

        # '종료' 액션
        exit_action = QAction('종료', self)
        exit_action.setShortcut('Ctrl+Q')
        exit_action.triggered.connect(self.close)

        # 메뉴에 액션들 추가
        file_menu.addActions([new_action, open_action, save_action, save_as_action])
        file_menu.addSeparator() # 구분선 추가
        file_menu.addAction(exit_action)

        # 편집 메뉴 생성
        edit_menu = menubar.addMenu('편집(&E)')

        # '실행 취소' 액션
        undo_action = QAction('실행 취소', self)
        undo_action.setShortcut('Ctrl+Z')
        undo_action.triggered.connect(self.text_edit.undo)

        # '다시 실행' 액션
        redo_action = QAction('다시 실행', self)
        redo_action.setShortcut('Ctrl+Y')
        redo_action.triggered.connect(self.text_edit.redo)

        # '잘라내기' 액션
        cut_action = QAction('잘라내기', self)
        cut_action.setShortcut('Ctrl+X')
        cut_action.triggered.connect(self.text_edit.cut)

        # '복사' 액션
        copy_action = QAction('복사', self)
        copy_action.setShortcut('Ctrl+C')
        copy_action.triggered.connect(self.text_edit.copy)

        # '붙여넣기' 액션
        paste_action = QAction('붙여넣기', self)
        paste_action.setShortcut('Ctrl+V')
        paste_action.triggered.connect(self.text_edit.paste)

        # '모두 선택' 액션
        select_all_action = QAction('모두 선택', self)
        select_all_action.setShortcut('Ctrl+A')
        select_all_action.triggered.connect(self.text_edit.selectAll)

        # 메뉴에 편집 액션들 추가
        edit_menu.addActions([undo_action, redo_action])
        edit_menu.addSeparator()
        edit_menu.addActions([cut_action, copy_action, paste_action])
        edit_menu.addSeparator() # 붙여넣기와 모두 선택 사이에 구분선 추가
        edit_menu.addAction(select_all_action)

        # 창의 제목을 '메모장'으로 설정합니다.
        self.setWindowTitle('메모장')
        
        # 창의 위치와 크기를 설정합니다. (x, y, 너비, 높이)
        self.setGeometry(300, 300, 600, 500)
        
        # 창을 화면에 보여줍니다.
        self.show()

    def new_file(self):
        """ 새 파일: 텍스트 에디터를 비웁니다. """
        self.text_edit.clear()
        self.current_file = None
        self.setWindowTitle('메모장')

    def open_file(self):
        """ 파일 열기: 파일 대화상자를 열고 선택한 파일의 내용을 불러옵니다. """
        fname, _ = QFileDialog.getOpenFileName(self, '파일 열기', '', '텍스트 파일 (*.txt);;모든 파일 (*.*)')
        if fname:
            with open(fname, 'r', encoding='utf-8') as f:
                self.text_edit.setText(f.read())
            self.current_file = fname
            self.setWindowTitle(f'{fname} - 메모장')

    def save_file(self):
        """ 파일 저장: 현재 파일이 있으면 덮어쓰고, 없으면 '다른 이름으로 저장'을 호출합니다. """
        if self.current_file:
            with open(self.current_file, 'w', encoding='utf-8') as f:
                f.write(self.text_edit.toPlainText())
        else:
            self.save_as_file()

    def save_as_file(self):
        """ 다른 이름으로 저장: 파일 대화상자를 열고 내용을 새 파일에 저장합니다. """
        fname, _ = QFileDialog.getSaveFileName(self, '다른 이름으로 저장', '', '텍스트 파일 (*.txt);;모든 파일 (*.*)')
        if fname:
            with open(fname, 'w', encoding='utf-8') as f:
                f.write(self.text_edit.toPlainText())
            self.current_file = fname
            self.setWindowTitle(f'{fname} - 메모장')

if __name__ == '__main__':
    # QApplication: 프로그램을 실행하고 이벤트 루프를 관리하는 클래스
    app = QApplication(sys.argv)
    
    # 우리가 만든 Notepad 클래스의 인스턴스를 생성합니다.
    notepad = Notepad()
    
    # 프로그램을 실행하고, 창을 닫을 때 프로세스가 종료되도록 합니다.
    sys.exit(app.exec())
