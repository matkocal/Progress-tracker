import json
import os
import tkinter as tk

#nazov json suboru
json_data = "progress_values.json"

#Funkcia na citanie zaznamov
def nacitaj_zaznamy():
    if os.path.exists(json_data):
        with open(json_data, "r", encoding="utf-8") as data:
            return json.load(data)
    else:
        return []

# Funkcia na ulozenie zaznamov
def uloz_zaznamy(zaznamy):
    with open(json_data, "w", encoding="utf-8") as data:
        json.dump(zaznamy, data, indent=4, ensure_ascii=False)

#INPUT hodnôť
while True:
    try:
        datum = input("zadaj datum (YYYY-MM-DD): ")
        cislo = int(input("zadaj číslo napredovania (1-20): "))
    
        if cislo in range(1, 21):
            zaznamy = nacitaj_zaznamy()
        
        # Pridanie zaznamov
            novy_zaznam = {
                "datum": datum,
                "cislo": cislo
            }
        
            zaznamy.append(novy_zaznam)
            uloz_zaznamy(zaznamy)
        
            print(f"Uložené: {datum}, číslo {cislo}")
            break
        else:
            print("nekompatibilný údaj")
            print("Skús znova...\n")
         
    except ValueError:
        print("Musíš zadať číslo")
        print("Skús znova...\n")
    
#funkcia na vymazanie dat
def vymaz_data():
    if os.path.exists(json_data):
        os.remove(json_data)
        print("Dáta vymazané")
        main.destroy()
    else:
        print("Žiadne dáta na vymazanie.")
        

#GRAF
main = tk.Tk()
main.title("Progress Tracker")
main.geometry("701x501")
main.minsize(700, 500)

# tlacidlo reset
reset_buttom = tk.Button(main, text= "Reset Data", command=vymaz_data, bg="black", fg="black",
                         font=("Arial", 12, "bold"))
reset_buttom.pack(pady=5)

canvas = tk.Canvas(main, bg="white", width=701, height=501)
canvas.pack(fill=tk.BOTH, expand=True)

grid_size = 19
margin = 20

grid_width = 750 - 2 * margin
grid_height = 550 -2 * margin

# kreslenie vertikalnych a hrubych ciar
for i, x in enumerate(range(0, 600, grid_size)):
    if i % 3 == 0:
        canvas.create_line(x, 0, x, 400, fill="black")
    else:
        canvas.create_line(x, 0, x, 400, fill="lightgrey")

for i, y in enumerate(range(0, 400, grid_size)):
    if i % 3 == 0:
        canvas.create_line(0, y, 600, y, fill="black")
    else:
        canvas.create_line(0, y, 600, y, fill="lightgrey")

# Vykreslenie bodov z JSON
zaznamy = nacitaj_zaznamy()

if zaznamy:
    # Zoradi zaznamy podla datumu
    zaznamy_sorted = sorted(zaznamy, key=lambda z: z["datum"])
    
    body = []
    for idx, zaznam in enumerate(zaznamy_sorted):  # OPRAVA: zaznam namiesto zaznamy
        # X pozícia = poradie záznamu (idx)
        # Y pozícia = číslo (1-10), ale obrátené (10 hore, 1 dole)
        x_pos = idx * grid_size + grid_size // 2
        y_pos = 400 - (zaznam["cislo"] * grid_size) + grid_size // 2
        
        # Nakresli bod 
        canvas.create_oval(x_pos - 5, y_pos - 5, x_pos + 5, y_pos + 5, 
                          fill="darkgreen", width=0.5)
        
        # OPRAVA: Pridaj bod do pola!
        body.append((x_pos, y_pos))
    
    # Spoji body ciarou
    if len(body) > 1:
        for i in range(len(body) - 1):
            canvas.create_line(body[i][0], body[i][1], body[i + 1][0], body[i + 1][1], 
                             fill="darkgreen", width=2)

main.mainloop()
