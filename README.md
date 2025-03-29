# mans_projekts
import tkinter as tk
from tkinter import messagebox
questions = [ 
    {"question": "Kurā gadā Latvija hokeja izlase pirmo reizi piedalījās Pasaules čempionātā pēc neatkarības atgūšanas?",
     "options": ["1990", "1997", "1994", "1992"],
     "answer": "1992"},
    {"question": "Kurš ir Latvijas hokeja izlases visu laiku rezultatīvākais spēlētājs?",
     "options": ["Kaspars Daugaviņš", "Helmuts Balderis", "Sandis Ozoliņš", "Leonīds Tambijevs"],
     "answer": "Leonīds Tambijevs"},
    {"question": "Kurš ir mūsu izlases galvenais treneris?",
     "options": ["Artis Ābols", "Artūrs Irbe", "Harijs Vītoliņš", "Aigars Kalvītis"],
     "answer": "Harijs Vītoliņš"}
     {"question": "Kurš no mūsu hokejistiem ir izcīnījis Stenlija kausu?",
     "options": ["Sandis Ozoliņš", "Sergejs Žoltoks", "Kārlis Skrastiņš", "Artūrs Irbe"],
     "answer": "Sandis Ozoliņš"}
     {"question": "Kāda ir Latvijas izlases lielākā uzvara Pasaules čempionātā?",
     "options": ["21 : 1", "15 : 2", "27 : 0", "32 : 0"],
     "answer": "32 : 0"}
     {"question": "Cik Olimpiskajās spēlēs ir piedalījusies Latvijas hokeja izlase?",
     "options": ["2", "6", "8", "1"],
     "answer": "6"} ]
class Hockeytest:
    def __init__(self, root):
        self.root = root
        self.root.title("Latvijas hokeja izlases tests")
        self.root.geometry("600x500")
        self.root.configure(bg="#800000")
        self.current_question = 0
        self.score = 0
        self.setup_ui()
    def setup_ui(self):
        self.label = tk.Label(self.root, text="Latvijas hokeja izlases tests", font=("Arial", 20, "bold"), fg="white", bg="#800000")
        self.label.pack(pady=20)
        self.start_button = tk.Button(self.root, text="Sākt testu", font=("Arial", 14), bg="#ffffff", fg="#800000", width=15, command=self.start_quiz)
        self.start_button.pack()
    def start_quiz(self):
        self.start_button.pack_forget()
        self.show_question()
    def show_question(self):
        if self.current_question < len(questions):
            question_data = questions[self.current_question]
            self.label.config(text=question_data["question"], font=("Arial", 16, "bold"))
            self.var = tk.StringVar()
            self.var.set(None)
            if hasattr(self, 'options_frame'):
                self.options_frame.destroy()
            self.options_frame = tk.Frame(self.root, bg="#800000")
            self.options_frame.pack()
            for option in question_data["options"]:
                tk.Radiobutton(self.options_frame, text=option, variable=self.var, value=option, font=("Arial", 14), bg="#800000", fg="white", selectcolor="black").pack(anchor="w", pady=5)
            if hasattr(self, 'submit_button'):
                self.submit_button.destroy()
            self.submit_button = tk.Button(self.root, text="Iesniegt", font=("Arial", 14), bg="#ffffff", fg="#800000", width=15, command=self.check_answer)
            self.submit_button.pack(pady=10)
        else:
            self.show_results()
    def check_answer(self):
        selected_answer = self.var.get()
        if selected_answer == questions[self.current_question]["answer"]:
            self.score += 1
        self.current_question += 1
        self.show_question()
    def show_results(self):
        messagebox.showinfo("Tests pabeigts", f"Jūsu rezultāts: {self.score}/{len(questions)}")
        self.root.quit()
if __name__ == "__main__":
    root = tk.Tk()
    app = Hockeytest(root)
    root.mainloop()