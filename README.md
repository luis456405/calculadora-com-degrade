import tkinter as tk

def criar_degrade(canvas, width, height, cor1, cor2):
    for i in range(height):
        cor_intermediaria = f"#{int(cor1[0] + (cor2[0] - cor1[0]) * i / height):02x}" \
                            f"{int(cor1[1] + (cor2[1] - cor1[1]) * i / height):02x}" \
                            f"{int(cor1[2] + (cor2[2] - cor1[2]) * i / height):02x}"
        canvas.create_line(0, i, width, i, fill=cor_intermediaria)

def realizar_operacao(operacao):
    try:
        num1 = float(entrada_num1.get())
        num2 = float(entrada_num2.get())
        if operacao == "+":
            resultado = num1 + num2
        elif operacao == "-":
            resultado = num1 - num2
        elif operacao == "*":
            resultado = num1 * num2
        elif operacao == "/":
            if num2 != 0:
                resultado = num1 / num2
            else:
                resultado = "Erro: Divisão por 0"
        label_resultado.config(text=f"Resultado: {resultado}", fg="white")
    except ValueError:
        label_resultado.config(text="Erro: Entrada inválida!", fg="red")

def limpar():
    entrada_num1.delete(0, tk.END)
    entrada_num2.delete(0, tk.END)
    label_resultado.config(text="Resultado:")

def sair():
    root.destroy()

# Configuração da Janela Principal
root = tk.Tk()
root.title("Calculadora Automática com Degradê")
root.geometry("400x600")  # Redimensiona a janela principal

# Criando o Canvas para o Degradê
canvas = tk.Canvas(root, width=400, height=600, highlightthickness=0)
canvas.pack(fill="both", expand=True)

# Criando o degradê
cor_preto = (0, 0, 0)
cor_azul = (0, 0, 255)
criar_degrade(canvas, 400, 600, cor_preto, cor_azul)

# Adicionando Widgets Interativos
label_num1 = tk.Label(root, text="Número 1:", font=("Arial", 12), bg="black", fg="white")
canvas.create_window(200, 50, window=label_num1)

entrada_num1 = tk.Entry(root, width=10, font=("Arial", 16))
canvas.create_window(200, 80, window=entrada_num1)

label_num2 = tk.Label(root, text="Número 2:", font=("Arial", 12), bg="black", fg="white")
canvas.create_window(200, 120, window=label_num2)

entrada_num2 = tk.Entry(root, width=10, font=("Arial", 16))
canvas.create_window(200, 150, window=entrada_num2)

# Botões de Operações
botao_somar = tk.Button(root, text="Somar", command=lambda: realizar_operacao("+"), bg="white", fg="black", font=("Arial", 12))
canvas.create_window(100, 200, window=botao_somar)

botao_subtrair = tk.Button(root, text="Subtrair", command=lambda: realizar_operacao("-"), bg="white", fg="black", font=("Arial", 12))
canvas.create_window(300, 200, window=botao_subtrair)

botao_multiplicar = tk.Button(root, text="Multiplicar", command=lambda: realizar_operacao("*"), bg="white", fg="black", font=("Arial", 12))
canvas.create_window(100, 250, window=botao_multiplicar)

botao_dividir = tk.Button(root, text="Dividir", command=lambda: realizar_operacao("/"), bg="white", fg="black", font=("Arial", 12))
canvas.create_window(300, 250, window=botao_dividir)

# Botões adicionais
botao_limpar = tk.Button(root, text="Limpar", command=limpar, bg="white", fg="black", font=("Arial", 12))
canvas.create_window(200, 300, window=botao_limpar)

botao_sair = tk.Button(root, text="Sair", command=sair, bg="white", fg="black", font=("Arial", 12))
canvas.create_window(200, 350, window=botao_sair)

# Label para mostrar o resultado
label_resultado = tk.Label(root, text="Resultado:", font=("Arial", 14), bg="black", fg="white")
canvas.create_window(200, 400, window=label_resultado)

root.mainloop()
