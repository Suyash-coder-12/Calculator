            '4', '5', '6', '-',
            '1', '2', '3', '+',
            '0', '.', '⌫', '='
        ]
        row_val = 1
        col_val = 0
        for button in buttons:
            btn = tk.Button(self, text=button, font=("Helvetica", 24), bg="#333333", fg="#FFFFFF", bd=0, command=lambda b=button: self.on_button_click(b))
            btn.grid(row=row_val, column=col_val, sticky="nsew", padx=5, pady=5)
            col_val += 1
            if col_val > 3:
                col_val = 0
                row_val += 1
        # Configure grid weights
        for i in range(5):
            self.grid_rowconfigure(i, weight=1)
            self.grid_columnconfigure(i, weight=1)
    def on_button_click(self, char):
        if char == 'C':
            self.display_var.set('')
        elif char == '⌫':
            current_text = self.display_var.get()
            self.display_var.set(current_text[:-1])
        elif char == '=':
            try:
                expression = self.display_var.get().replace('×', '*')  # Replace × with *
                result = eval(expression)
                self.display_var.set(result)
            except Exception as e:
                self.display_var.set('Error')
        else:
            current_text = self.display_var.get()
            self.display_var.set(current_text + char)
if __name__ == "__main__":
    app = Calculator()
    app.mainloop()
