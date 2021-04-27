# Python-Practice _ 메모장
import os
from tkinter import *

root = Tk()
root.title("제목 없음 - 메모장")
root.geometry("400x400")

filename = "note.txt"

def open_file():
    if os.path.isfile(filename):
        with open(filename, "r", encoding="utf8") as file:
            txt.delete("1.0", END)
            txt.insert(END, file.read())

def save_file():
    with open(filename, "w", encoding="utf8") as file:
        file.write(txt.get("1.0", END))

menu = Menu(root)

# 파일
menu_file = Menu(menu, tearoff=0)
menu_file.add_command(label="새로 만들기(N)")
menu_file.add_command(label="열기(O)", command = open_file)
menu_file.add_command(label=" 저장(S)", command = save_file)
menu_file.add_command(label="다른 이름으로 저장(A)")
menu_file.add_separator()
menu_file.add_command(label="페이지 설정(U)")
menu_file.add_command(label="인쇄(P)")
menu_file.add_separator()
menu_file.add_command(label="끝내기(X)", command=root.quit)
menu.add_cascade(label="파일(F)", menu=menu_file)

# 편집
menu_edit = Menu(menu, tearoff=0)
menu_edit.add_command(label="실행취소(U)")
menu_edit.add_separator()
menu_edit.add_command(label="복사(C)")
menu_edit.add_command(label="붙여넣기(P)")
menu.add_cascade(label="편집(E)", menu=menu_edit)
#서식
menu_format = Menu(menu, tearoff=0)
menu_format.add_checkbutton(label="자동 줄 바꿈(W)")
menu_format.add_checkbutton(label="글꼴(F)")
menu.add_cascade(label="서식(O)", menu=menu_format)
#보기
menu_view = Menu(menu, tearoff=0)
menu_view.add_command(label="상태 표시줄(S)", state="disable")
menu.add_cascade(label="보기(V)", menu=menu_view)
#도움말
menu_help = Menu(menu, tearoff=0)
menu_help.add_command(label="도움말 보기(H)")
menu_help.add_separator()
menu_help.add_command(label="메모장 정보(A)")
menu.add_cascade(label="도움말(H)", menu=menu_help)

# 스크롤바
scrollbar = Scrollbar(root)
scrollbar.pack(side="right", fill="y")

txt = Text(root, yscrollcommand=scrollbar.set)
txt.pack(side="left", fill="both", expand=True)

scrollbar.config(command=txt.yview)
root.config(menu=menu)
root.mainloop()
