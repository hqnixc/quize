import tkinter as tk
from tkinter import messagebox

# Вопросы и ответы
questions = [
    {"question": "Когда тебя ебали, что на жопе написали?", 
     "answers": ["Жопа-не бумага, хуй-не карандаш", "Твоё имя", "Там было чисто"],
     "correct": "Жопа-не бумага, хуй-не карандаш"},

    {"question": "Есть два стула, на одном пики точены, на другом хуи дрочены, на какой сядешь, на какой мать посадишь?", 
     "answers": ["Сяду на пики, маму на хуи", "Возьму пики точены, срублю хуи", "Сяду на хуи, мама разберётся сама"], 
     "correct": "Возьму пики точены, срублю хуи"},

    {"question": "Ты упал в яму. В яме пирожок и хуй. Что съешь, что в жопу засунешь?", 
     "answers": ["Съем пирожок, засуну хуй", "Возьму пирожок и вылезу из ямы", "Буду плакать"], 
     "correct": "Возьму пирожок и вылезу из ямы"},

     {"question": "Ты летишь на парашюте, справа - лес хуев, слева - море говна. Куда будешь садиться?", 
     "answers": ["Лес хуев", "В каждом лесу есть поляна, а в каждом море - островок", "Куда ветер дунет-туда и приземлюсь"], 
     "correct": "В каждом лесу есть поляна, а в каждом море - островок"},

     {"question": "В жопу дашь или мать продашь?", 
     "answers": ["Мать продам и убегу", "Мать-святое, дам в жопу", "Жопа не дается, мать не продаётся"], 
     "correct": "Жопа не дается, мать не продаётся"},

     {"question": "Что сьешь - мыло со стола или хлеб с параши?", 
     "answers": ["Стол не мыльница, параша не хлебница", "Уроню мыло и наклонюсь, чтобы его поднять", "Мыло со стола"], 
     "correct": "Стол не мыльница, параша не хлебница"},

     {"question": "Ты с кентом идешь по пустыне Сахаре. На расстоянии ста километров нет ни жилья, ни населенных пунктов, никого и ничего, кроме песка. Вдруг выползает ядовитая змея, бросается на кента и кусает его за хуй. Что делать будешь?", 
     "answers": ["Отсосу яд, я же хороший друг", "Убегу, чтобы меня тоже не укусила", " Если у кента залупа выше колена, то змея не достанет. Если ниже - то он сам отсосет."], 
     "correct": " Если у кента залупа выше колена, то змея не достанет. Если ниже - то он сам отсосет."}
]

class QuizApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Тест на льва")
        self.current_question = 0
        self.correct_answers = 0

        self.question_label = tk.Label(root, text="", font=("Arial", 14), wraplength=400)
        self.question_label.pack(pady=10)

        self.buttons = []
        for _ in range(3):  
            btn = tk.Button(root, text="", font=("Arial", 12), command=lambda b=_: self.check_answer(b))
            btn.pack(pady=5, fill="x")
            self.buttons.append(btn)

        self.next_question()

    def next_question(self):
        if self.current_question < len(questions):
            q_data = questions[self.current_question]
            self.question_label.config(text=q_data["question"])
            for i, btn in enumerate(self.buttons):
                btn.config(text=q_data["answers"][i], state="normal")
        else:
            messagebox.showinfo("Результат", f"Ты ответил(а) правильно на {self.correct_answers} из {len(questions)} вопросов!")
            self.root.quit()

    def check_answer(self, btn_index):
        q_data = questions[self.current_question]
        if self.buttons[btn_index].cget("text") == q_data["correct"]:
            self.correct_answers += 1
            messagebox.showinfo("Правильно!", "Ай, что за тигр!")
        else:
            messagebox.showerror("Неправильно", "Мда, петушок...")

        self.current_question += 1
        self.next_question()
def get_name():
    """Окно для ввода имени перед началом теста."""
    name_window = tk.Tk()
    name_window.title("Ввод имени")

    tk.Label(name_window, text="Как тебя зовут?", font=("Arial", 14)).pack(pady=10)
    
    name_entry = tk.Entry(name_window, font=("Arial", 12))
    name_entry.pack(pady=5)

    def start_quiz():
        user_name = name_entry.get().strip()
        if user_name:
            name_window.destroy()
            root = tk.Tk()
            QuizApp(root, user_name)
            root.mainloop()
        else:
            messagebox.showwarning("Ошибка", "Введите имя!")

    tk.Button(name_window, text="Начать тест", font=("Arial", 12), command=start_quiz).pack(pady=10)
    
    name_window.mainloop()

# Запуск ввода имени перед тестом
get_name()

# Запуск квиза
root = tk.Tk()
quiz_app = QuizApp(root)
root.mainloop()
