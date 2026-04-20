# A-game-about-a-farm.
Hello, I've been missing. for a long time, for almost a month, I did this gigantic project, I did everything myself, not a single carbon copy with AI. Why abruptly? I only post global projects here, and the rest of the time I study and practice. 

```Python
import time
import sys
import json
import random

def print_slow(text, delay=0.01):
  for char in text:
   sys.stdout.write(char)
   sys.stdout.flush()
   time.sleep(delay) 
  print()
 

class game:
  def __init__(self):
    self.health = 100
    self.enemy_health = 0

    self.day = 0
    self.hours = 0
    self.days = ["MONDAY", "TUESDAY", "WEDNESDAY", "THURSDAY", "FRIDAY", "SATURDAY", "SUNDAY"]
    self.summer = False
    self.autumn = False
    self.winter = False
    self.spring = False
    self.money = 50
    self.inventory = []
    self.chest = []
    self.clear = False
    self.watering = False
    self.water = False
    self.fertilizer = False
    self.height = False
    self.ignore = 3
    self.watering_ignore = 2
    self.garden = []

    self.plant_growth = {
      "Carrot Seeds": 3,
      "Potato Tuber": 5,
      "Cabbage Seeds": 10,
      "Beet Seeds": 3,
      "Wheat Seeds": 2,
      "Sunflower Seeds": 20,
      "Tomato Seeds": 15,
      "Cucumber Seeds": 15,
      "Corn Seeds": 25,
      "Pumpkin Seeds": 32,
      "Bean Seeds": 15
    }

    self.luck1 = False

    self.assortment = {}

    self.sale_assortment = {
      "Carrot": 10,
      "Potato": 10,
      "Cabbage": 20,
      "Beet": 22,
      "Wheat": 10,
      "Sunflower": 40,
      "Tomato": 20,
      "Cucumber": 15,
      "Corn": 25,
      "Pumpkin": 55,
      "Bean": 30,
      "Sour Cream": 25,
      "Cheese": 50, 
      "Wool": 35,
      "Egg": 20,
      "Mayonnaise": 40,
      "Cottage Cheese": 60,
      "Stone": 5,
      "Iron Ore": 20,
      "Ruby": 150
    }

    self.remains = {
      "Wheat Seeds": 5,
      "Carrot Seeds": 5,
      "Cabbage Seeds": 5,
      "Beet Seeds": 5,
      "Pumpkin Seeds": 5,
      "Cucumber Seeds": 5,
      "Corn Seeds": 5,
      "Tomato Seeds": 5,
      "Bean Seeds": 5,
      "Fertilizer": 5
    }

    self.facts = {
      "\nTip/Fact: Our fertilizer reduces plant growth time by 5 days and does not harm the sprout.\n"
      "\nTip/Fact: You should visit that white mansion, it's not some millionaire's house but a universal store where our friends from the village will build everything from a chicken coop to a pigsty cheaply and with quality. You can also buy tools there!\n"
      "\nTip/Fact: Plants will dry out after 5 days without watering, all at once.\n"
      "\nTip/Fact: There's a cave nearby, but be careful. No one knows what's going on in there...\n"
      "\nTip/Fact: When winter comes, all plants die. Harvest everything in time!\n"
      "\nTip/Fact: Our seeds are obtained by hand, not from a factory.\n"
      "\nTip/Fact: Your garden overgrows every 3 days.\n"
      "\nTip/Fact: There are few beetles in our region, it's not a problem at all.\n"
      "\nTip/Fact: Seeds change throughout the seasons, and are not sold at all in winter.\n"
    }

    self.facts2 = {
      "\nHey, did you know that in the white mansion they give male animals as a gift?\n"
      "\nHey, we think sellers raise prices too much...\n"
      "\nHey, why are you asking? We're just fools!...\n"
      "\nHey, birds are our saviors... I'm sure! They're dinosaurs...\n"
      "\nHey, I wonder why stones are hard...\n"
      "\nHey, you can make sour cream from milk and starter...\n"
      "\nHey, the chicken coop is the best thing to buy at first, it allows you to cook, unlike the cowshed or sheepfold...\n"
      "\nHey, the weather is terrible today...\n"
      "\nHey, I recommend visiting the cave! There are precious gems on the 20th floor, but it's very hard to get there, sell stones, iron, and rubies at the Everything for Five store...\n"
    }

    self.mining_case = 0
    self.battle = False
    self.floor = 0
    self.pickaxe1 = False
    self.pickaxe2 = False
    self.pickaxe3 = False
    self.pickaxe4 = False

    self.animals = {
      "Chicken",
      "Cow",
      "Sheep"
    }


    self.egg_production = 0
    self.milk_production = 0
    self.wool_production = 0

    self.chicken_count = 0
    self.cow_count = 0
    self.sheep_count = 0


    self.hencoop_built = False
    self.hencoop = {
      "Rooster": 1
    }

    self.cowshed_built = False
    self.cowshed = {
      "Bull": 1
    }
    self.sheepfold_built = False
    self.sheepfold = {
      "Ram": 1
    }

    self.eggs_on = 0
    self.milk_on = 0
    self.wool_on = 0

    self.barrel = {}


    self.gift_give_1 = False
    self.gift_give_2 = False

    self.process1 = False
    self.process2 = False
    self.process3 = False
    self.process4 = False
    self.process5 = False
    self.process6 = False
    self.process7 = False

    self.record1 = 0
    self.record2 = 0
    self.record3 = 0
    self.record4 = 0
    self.record5 = 0
    self.record6 = 0
    self.record7 = 0
    self.record8 = 0

    self.mayonnaise = False
    self.cheese = False
    self.sour_cream = False
    self.curd = False

    self.assortment_2 = {
      "Dynamite": 40,
      "Aluminum Pickaxe": 40,
      "Iron Pickaxe": 70,
      "Steel Pickaxe": 150
    }

    self.ingredient_egg = False
    self.ingredient_milk = False
    self.ingredient_sourdough = False
    self.ingredient_sour_cream = False

    self.dynamite_assortment = 10

  
  
  def menu(self): 
    print_slow("="*58, 0.01)
    print_slow("MAIN MENU\n", 0.03)
    print_slow("CHOOSE ACTION NUMBER: \n", 0.01)
    print_slow("1. PLAY\n\n", 0.01)
    print_slow("2. INSTRUCTIONS (recommended.)\n\n", 0.01)
    print_slow("3. SAVES\n\n", 0.01)
    print_slow("4. EXIT", 0.01)
    print_slow("="*58, 0.01)
    while True:
      try:
        menu_choice = input("\nINPUT: ").lower().strip()
        if menu_choice == "1":
          self.game_start()
          break
        elif menu_choice == "2":
          self.instructions()
          break
        elif menu_choice == "3":
          self.preservation()
          break
        elif menu_choice == "4":
          confirmation = input("Are you sure you want to exit? yes/no: ").lower().strip()
          if confirmation == "yes":
            print("\ngoodbye!\n\n")
            time.sleep(2)
            exit()
            break
          else:
            print("Returning back...")
            time.sleep(2)
            continue
      except:
        input("Incorrect, enter the number of your action.\nPress Enter to try again.")
        continue

  def game_start(self):
    print_slow("\nRoutine... you're tired of working as a cashier...\n", 0.05)
    print_slow("Coming home, you saw under your doormat...", 0.07)
    time.sleep(2)
    print_slow("yes, under the doormat, you saw something like there's something under it... A folder with a note and a document...\n", 0.07)
    time.sleep(0.2)
    print_slow("Nephew... hello. \nI recently paid off the mortgage on that house...\nAll this time I've been living on the farm, remember when you were here as a child?\nI realized that you can be responsible for this. I'm giving it to you, I know you're tired of routine work.\nhere's your salvation! farm! good luck with the farming...\nYour Aunt Jael...")
    print_slow("\nYOU: ...", 0.05)
    time.sleep(0.2)
    print_slow("\nYOU: I'm really tired... I've been working as a salesman for almost 6 months...", 0.03)
    print_slow("You went to sleep...", 0.05)
    time.sleep(2)
    print_slow("\nAfter 3 days, you arrived at the address listed in the documents...\n", 0.06)
    print_slow("\nA trampled garden, aunt was apparently more busy with finances than farming.", 0.03)
    time.sleep(1)
    print_slow("\nThe house is small. It looks a bit like a barn, next to it you see an overgrown path blocked by a wooden sign, you throw a stone and the sign falls.", 0.03)
    print_slow("\nYou entered the house... need to make a lock.", 0.05)
    print("You fell asleep on the bed immediately...")
    if not self.gift_give_1:
      print_slow("\nNEW ITEMS: SCYTHE, PICKAXE, WATERING CAN\n")
      self.add_inventory("Scythe")
      print("\n")
      self.add_inventory("Pickaxe")
      print("\n")
      self.add_inventory("Watering Can")
      print("\n")
      self.gift_give_1 = True
    if not self.gift_give_2:
      print_slow("==Wait for the fifth day...==\n")
      print("\n")
    self.new_day()
  
  def loop(self):
    if self.check_sleep():
      return
    while True:
      print("ACTIONS OUTSIDE:")
      print_slow("\n1. Enter the house")
      print_slow("\n2. Go along the path")
      print_slow("\n3. Go to your garden")
      print_slow("\n4. Go to buildings")
      print_slow("\n5. Quick menu")
      print("\nWhat do you choose?")
      
      while True:
        question = input("INPUT: ").strip().lower()
        if question == "1":
          print_slow("\nDoor creaks...\n\n", 0.05)
          self.hours += 0.05
          self.home()
          break
        elif question == "2":
          self.hours += 0.05
          self.pathway()
          break
        elif question == "3":
          print("\nHere's your garden!\n\n")
          
          self.hours += 0.05
          self.garden_open()
          break
        elif question == "4":
          if self.hencoop_built == False and self.cowshed_built == False and self.sheepfold_built == False:
            print_slow("\nYou don't have any buildings yet!.\n", 0.01)
            time.sleep(1)
          else:
            print_slow("\nYOUR BUILDINGS: \n\n")
            self.buildings()
          break

            
            
        elif question == "5":
          self.fast_menu()
          break
        elif question == "inventory":
          self.inventory_open()
          self.hours += 0.05
          continue
        elif question == "time":
          print(f"{self.hours} hours")
          continue
        
  def pathway(self):
    print_slow("You went along this strange path...", 0.03)
    if self.winter == False and self.luck1 == True:
      find = random.randint(1, 20)
      if find == 5:
        print_slow("You found a carrot seed!", 0.01)
        self.luck1 = False
        print_slow("Write 1 - to take, 2 - to pass by.")
        while True:
          try:
            question =  input("INPUT: ").lower().strip()
            if question == "1":
              print_slow("You took the carrot seed, it can grow.")
              self.add_inventory("Carrot Seeds")
              time.sleep(1)
              self.pathway_loop()
              return
            elif question == "2":
              print_slow("You passed by...")
              time.sleep(1)
              self.pathway_loop()
              return
            elif question == "inventory":
              print(self.inventory)
              self.hours += 0.05
              continue
            elif question == "time":
              print(f"{self.hours} hours")
              continue
          except:
            input("Incorrect, enter the number of your action.\nPress Enter to try again.")
            continue

      elif find == 10:
        print_slow("You found a potato tuber!", 0.01)
        self.luck1 = False
        print_slow("Write 1 - to take, 2 - to pass by.")
        while True:
          try:
            question =  input("INPUT: ").lower().strip()
            if question == "1":
              print_slow("You took the potato tuber, it smells like earth!.")
              self.add_inventory("Potato Tuber")
              time.sleep(1)
              self.pathway_loop()
              return
            
            elif question == "2":
              print_slow("You passed by...")
              time.sleep(1)
              self.pathway_loop()
              return
            
            elif question == "inventory":
              print(self.inventory)
              self.hours += 0.05
              continue

            elif question == "time":
              print(f"{self.hours} hours")
              continue

          except:
            input("Incorrect, enter the number of your action.\nPress Enter to try again.")
            continue

        

      elif find == 15:
        print_slow("You found a cabbage seed!", 0.01)
        self.luck1 = False
        print_slow("Write 1 - to take, 2 - to pass by.")
        while True:
          try:
            question =  input("\nINPUT: ").lower().strip()
            if question == "1":
              print_slow("You took the cabbage seed, it's bright.")
              self.add_inventory("Cabbage Seeds")
              time.sleep(1)
              self.pathway_loop()
              return
            
            elif question == "2":
              print_slow("You passed by...")
              time.sleep(1)
              self.pathway_loop()
              return
            
            elif question == "inventory":
              print(self.inventory)
              self.hours += 0.05
              continue

            elif question == "time":
              print(f"{self.hours} hours")
              continue

          except:
            input("Incorrect, enter the number of your action.\nPress Enter to try again.")
            continue

      elif find == 20:
        print_slow("You found a sunflower seed!", 0.01)
        self.luck1 = False
        print_slow("Write 1 - to take, 2 - to pass by.")
        while True:
          try:
            question =  input("INPUT: ").lower().strip()
            if question == "1":
              print_slow("You took the sunflower seed, good sprout!.")
              self.add_inventory("Sunflower Seeds")
              time.sleep(1)
              self.pathway_loop()
              return
      
            
            elif question == "2":
              print_slow("You passed by...")
              time.sleep(1)
              self.pathway_loop()
              return
            
            elif question == "inventory":
              print(self.inventory)
              self.hours += 0.05
              continue

            elif question == "time":
              print(f"{self.hours} hours")
              continue

          except:
            input("Incorrect, enter the number of your action.\nPress Enter to try again.")
            continue
      else:
        self.pathway_loop()
    else:
      self.pathway_loop()  

  def pathway_loop(self):
    print_slow("\nYOU ARE IN THE VILLAGE", 0.01)
    while True:
      print_slow("\n\nWHERE DO YOU WANT TO GO:\n 1 - TO THE STORE\n 2 - GO FURTHER\n 3 - TALK TO PASSERSBY\n 4 - TO THE WHITE MANSION \n 5 - LEAVE.")
      try: 
        question = input("INPUT: ").lower().strip()
        if question == "1":
          print_slow("You approach the store...", 0.02)
         
          time.sleep(1)
          print_slow("\nSELLER: Welcome to the 'Everything for Five' store! Here's our assortment!\n==PRICE PER PIECE==\n\n")
          self.assortment.clear()
          assortiment1 = random.randint(1, 3)

          if assortiment1 == 1:
            self.assortment["Wheat Seeds"] = 5
          elif assortiment1 == 2:
            self.assortment["Carrot Seeds"] = 5
          else:
            self.assortment["Bean Seeds"] = 15
          

          assortiment2 = random.randint(1, 3)
          
          if assortiment2 == 1:
            self.assortment["Cabbage Seeds"] = 10
          elif assortiment2 == 2:
            self.assortment["Beet Seeds"] = 10
          else:
            pass


          assortiment3 = random.randint(1, 3)
          
          if assortiment3 == 1:
            self.assortment["Pumpkin Seeds"] = 20
          elif assortiment3 == 2:
            self.assortment["Cucumber Seeds"] = 10
          else:
            pass


          assortiment4 = random.randint(1, 3)
          
          if assortiment4 == 1:
            self.assortment["Corn Seeds"] = 25
          elif assortiment4 == 2:
            self.assortment["Tomato Seeds"] = 10
          else:
            pass

          assortiment5 = 1
          
          if assortiment5 == 1:
            self.assortment["Fertilizer"] = 30

          for item, price in self.assortment.items():
            print(f"{item} - {price}$.")

          print_slow("\nWHAT DO YOU WANT TO DO?: \n1. BUY SOMETHING.\n2. SELL SOMETHING.\n3. LEARN AN INTERESTING FACT. \n 4. LEAVE\n", 0.005)
          while True:
            try:
              question = input("\nINPUT: ").strip().capitalize()
              if question == "1":
                if self.winter == False:
                  print_slow("ENTER THE EXACT NAME OF WHAT YOU WANT TO BUY (example: Corn Seeds)", 0.005)
                  while True:
                    try:
                      purchase = input("\nINPUT: ").lower().strip()
                      
                      found = False
                      for item in self.assortment:
                        if item.lower() == purchase.lower():
                          price = self.assortment[item]
                          purchase = item
                          found = True
                          break

                      if found:

                        print_slow("\npurchase: ENTER THE QUANTITY OF GOODS YOU WANT TO PURCHASE.", 0.009)
                        quantity = int(input("\nINPUT: "))
                        if quantity > 5:
                          print_slow("\nLIMIT REACHED. YOU CAN ONLY BUY 5 PIECES AT A TIME.\n")
                        else:
                          if purchase in self.remains:
                            if quantity > self.remains[purchase]:
                              print_slow("\nNot enough in stock\n")
                            else:
                              self.remains[purchase] -= quantity
                              if self.remains[purchase] == 0:
                                self.rem_remains(purchase)
                          total_price = (price * quantity)
                          print_slow(f"TOTAL PRICE: {total_price}$\n")
                          print_slow("PROCESSING...\n", 0.005)
                          time.sleep(1)
                          if self.money >= total_price:
                            print("Purchased!")
                            self.money -= total_price
                            self.add_inventory(purchase)
                            print(f"You have {self.money}$ left")
                            break
                          else:
                            print("Not enough money!")
                            print(f"You have {self.money}$, need {total_price}$.\n")
                            continue
          
                      else:
                        print_slow("\nThis item is not available...")
            

                    except: 
                      input("Incorrect, enter the name of what you want to buy.\nPress Enter to try again.")
                      continue

                else:
                  print_slow("\n\nSELLER: Sorry, but seeds are not sold in winter... I recommend taking up animal husbandry.\n")
                continue

              elif question == "2":
                print_slow("\nHere's our sales assortment:\n")
                for sell_item, price in self.sale_assortment.items():
                  print(f"{sell_item} - {price} $.")

                print_slow("ENTER THE EXACT NAME OF WHAT YOU WANT TO SELL (example: Corn Seeds)", 0.005)
                while True:
                  try:
                    sale = input("\nINPUT: ").strip().capitalize()
                    if sale in self.sale_assortment:
                      print_slow("\nsale: ENTER THE QUANTITY OF GOODS YOU WANT TO SELL.", 0.009)
                      sale_quantity = int(input("\nINPUT: \n"))
                      payment = price * sale_quantity
                      print(f"\nThis is {payment}$\n")
                      for cell in self.inventory:
                        if cell["name"].lower() == sale.lower():
                          if cell["quantity"] >= sale_quantity:
                            cell["quantity"] -= sale_quantity
                            if cell["quantity"] == 0:
                              self.inventory.remove(cell)
                          payment = sale * price
                          self.money += payment
                          print(f"You have successfully been paid {payment}$.")
                          break
                      
                      else:
                        print("\nYou don't have that item...\n\n")
                        continue
                  except:
                    input("Incorrect, enter the name of what you want to sell.\nPress Enter to try again.")
                    continue

              
              elif question == "3":
                print(random.choice(list(self.facts.values())))
                continue

              elif question == "4":
                print("You left...")
                break
                

                

              elif question == "inventory":
                print(self.inventory)
                self.hours += 0.05
                continue

              elif question == "time":
                print(f"{self.hours} hours")
                continue    



            except:
              input("Incorrect, enter the number of your action.\nPress Enter to try again.")
              continue


        elif question == "2":
          print("You go further...")
          print_slow("WHERE DO YOU WANT TO GO? \n1. Small stone shed \n2. Cave \n3. Leave")
          while True:
            try:
              question = input("INPUT: \n").lower().strip()
              if question == "1":
                print_slow("\nYou enter, opening a creaky iron door...", 0.01)
                time.sleep(1)
                print_slow("\nSeller: welcome... or neutrally welcome to the 'Pickaxe Sharpness' store!\n")
                print_slow("Our assortment is simple...\n\n")
                for item, price in self.assortment_2.items():
                  print(f"{item} - {price}$\n")
                print_slow("\nSeller: what do you want to buy? (enter the name of what you want to buy.)\n.")
                print("\n=Write 5 to exit...=\n")
                while True:
                  try:
                    question = input("\nINPUT: ").lower().strip()
                    if question in ["dynamite", "1"]:
                      print_slow("\nSeller: I don't consider you a criminal, but I must remind you that dynamite can only be used in the cave following the rules.\n")
                      print_slow("Seller: how many sticks of dynamite do you want to buy? Our assortment replenishes up to 10 every day. Write Exit to exit.\n")
                      while True:
                        try:
                          quantity = int(input("\nINPUT: "))
                          if quantity > self.dynamite_assortment:
                            print_slow(f"Seller: sorry, but at the moment our assortment is: {self.dynamite_assortment} sticks of dynamite.")
                            continue
                            
                          else:
                            total_price = quantity * 40
                            print_slow(f"TOTAL PRICE: {total_price}")
                            print_slow("PROCESSING...\n", 0.005)
                            if self.money >= total_price:
                              print("Purchased!")
                              self.money -= total_price
                              self.add_inventory("Dynamite", quantity)
                              print(f"You have {self.money}$ left")
                              break
                            else:
                              print("Not enough money!")
                              print(f"You have {self.money}$, need {total_price}$.\n")
                              continue
                        
                        except:
                          input("Incorrect, enter the name of what you want to buy.\nPress Enter to try again.")
                          continue

                      print_slow("")


                    elif question == "Exit":
                      for item, price in self.assortment_2.items():
                        print(f"{item} - {price}$\n")
                      print_slow("\nSeller: what do you want to buy? (enter the name of what you want to buy.)\n.")
                      print("\n=Write 5 to exit...=\n")
                      break

                    elif question in ["aluminum pickaxe", "2"]:
                      for cell in self.inventory:
                        if cell["name"] == "Aluminum Pickaxe":
                          print("You already have an aluminum pickaxe...")
                          time.sleep(1)
                          break

                        else:
                          total_price = 40
                          print_slow("Seller: The purchase will cost 40$ \nDo you agree to the purchase? Yes/No: ")
                          while True:
                            try:
                              question = input("\nINPUT: ")
                              if question == "yes":
                                print_slow(f"TOTAL PRICE: {total_price}")
                                print_slow("PROCESSING...\n", 0.005)
                                if self.money >= total_price:
                                  print("Purchased!")
                                  self.money -= total_price
                                  self.add_inventory("Aluminum Pickaxe")
                                  print(f"You have {self.money}$ left")
                                  break
                                else:
                                  print("Not enough money!")
                                  print(f"You have {self.money}$, need {total_price}$.\n")
                                  continue
                              
                              elif question == "no":
                                break

                            except:
                              print("Incorrect, write yes or no depending on your choice. \nPress Enter to try again.")
                              continue

                    elif question in ["iron pickaxe", "3"]:
                      for cell in self.inventory:
                        if cell["name"] == "Iron Pickaxe":
                          print("You already have an iron pickaxe...")
                          time.sleep(1)
                          break

                        else:
                          total_price = 70
                          print_slow("Seller: The purchase will cost 70$ \nDo you agree to the purchase? Yes/No: ")
                          while True:
                            try:
                              question = input("\nINPUT: ")
                              if question == "yes":
                                print_slow(f"TOTAL PRICE: {total_price}")
                                print_slow("PROCESSING...\n", 0.005)
                                if self.money >= total_price:
                                  print("Purchased!")
                                  self.money -= total_price
                                  self.add_inventory("Iron Pickaxe")
                                  print(f"You have {self.money}$ left")
                                  break
                                else:
                                  print("Not enough money!")
                                  print(f"You have {self.money}$, need {total_price}$.\n")
                                  continue
                              
                              elif question == "no":
                                break

                            except:
                              print("Incorrect, write yes or no depending on your choice. \nPress Enter to try again.")
                              continue


                    elif question in ["steel pickaxe", "4"]:
                      for cell in self.inventory:
                        if cell["name"] == "Steel Pickaxe":
                          print("You already have a steel pickaxe...")
                          time.sleep(1)
                          break

                        else:
                          total_price = 150
                          print_slow("Seller: The purchase will cost 150$ \nDo you agree to the purchase? Yes/No: ")
                          while True:
                            try:
                              question = input("\nINPUT: ")
                              if question == "yes":
                                print_slow(f"TOTAL PRICE: {total_price}")
                                print_slow("PROCESSING...\n", 0.005)
                                if self.money >= total_price:
                                  print("Purchased!")
                                  self.money -= total_price
                                  self.add_inventory("Steel Pickaxe")
                                  print(f"You have {self.money}$ left")
                                  break
                                else:
                                  print("Not enough money!")
                                  print(f"You have {self.money}$, need {total_price}$.\n")
                                  continue
                              
                              elif question == "no":
                                break

                            except:
                              print("Incorrect, write yes or no depending on your choice. \nPress Enter to try again.")
                              continue

                    elif question == "5":
                      print_slow("WHERE DO YOU WANT TO GO? \n1. Small stone shed \n2. Cave \n3. Leave")
                      break
                      

                    elif question == "inventory":
                      print(self.inventory)
                      self.hours += 0.05
                      continue

                    elif question == "time":
                      print(f"{self.hours} hours")
                      continue

                    else:
                      print_slow("\nPerhaps you made a typo, write your choice correctly. Example: Aluminum Pickaxe \n")
                      time.sleep(1)
                      continue

                  except:
                    input("Incorrect, enter the number of your action.\nPress Enter to try again.")
                    continue

              elif question == "2":
                print_slow("\nYou entered the cave...")
                print_slow("\nCHOOSE YOUR EQUIPMENT (write the number of your choice, 4 - to exit):\n")
                if self.has_item("Pickaxe"):
                  print_slow("\n1. Pickaxe (Regular)")
                else:
                  print_slow("\n1. Pickaxe (Regular) - MISSING")

                if self.has_item("Aluminum Pickaxe"):
                  print_slow("\n2. Aluminum Pickaxe")
                else:
                  print_slow("\n2. Aluminum Pickaxe - MISSING")

                if  self.has_item("Iron Pickaxe"):
                  print_slow("\n3. Iron Pickaxe")
                else:
                  print_slow("\n3. Iron Pickaxe - MISSING")

                if self.has_item("Steel Pickaxe"):
                  print_slow("\n3. Steel Pickaxe")
                else:
                  print_slow("\n3. Steel Pickaxe - MISSING")
                
                while True:
                  try:
                    pickaxe_choice = input("\nINPUT: ").strip()
                    if pickaxe_choice == "1": 
                      if self.has_item("Pickaxe"):
                        self.pickaxe1 = False
                        self.pickaxe2 = False
                        self.pickaxe3 = False
                        self.pickaxe4 = False
                        self.pickaxe1 = True
                        print("Selected: regular Pickaxe.")
                      else:
                        print_slow("You don't have a regular pickaxe... did you change the code?\n")
                        continue

                    elif pickaxe_choice == "2":
                      if self.has_item("Aluminum Pickaxe"):
                        print("\nSelected: Aluminum Pickaxe.")
                        self.pickaxe1 = False
                        self.pickaxe2 = False
                        self.pickaxe3 = False
                        self.pickaxe4 = False
                        self.pickaxe2 = True
                        break
                      else:
                        print_slow("You don't have an aluminum pickaxe...")
                        time.sleep(1)
                        continue

                    elif pickaxe_choice == "3":
                      if self.has_item("Iron Pickaxe"):
                        print("\nSelected: Iron Pickaxe.")
                        self.pickaxe1 = False
                        self.pickaxe2 = False
                        self.pickaxe3 = False
                        self.pickaxe4 = False
                        self.pickaxe3 = True
                        break
                      else:
                        print_slow("You don't have an iron pickaxe...")
                        time.sleep(1)
                        continue

                    elif pickaxe_choice == "4":
                      if self.has_item("Steel Pickaxe"):
                        print("\nSelected: Steel Pickaxe.")
                        self.pickaxe1 = False
                        self.pickaxe2 = False
                        self.pickaxe3 = False
                        self.pickaxe4 = False
                        self.pickaxe4 = True
                        break
                      else:
                        print_slow("You don't have a steel pickaxe...")
                        time.sleep(1)
                        continue

                  except:
                    input("Incorrect, enter the number of your choice.\nPress Enter to try again.")
                    continue

                input("\n==Important: You can always press 5 to exit== \n==The better the pickaxe, the more often you find precious stones...== \n== There's a prize waiting for you on the 20th floor ==\n\n\n \n\nPress Enter if you've learned...\n")
                print_slow("You are in the cave... it's dark...")
                self.floor_cave()
  

              elif question == "3":
                print_slow("You leave...")
                break

            except:
              input("Incorrect, enter the number of your action.\nPress Enter to try again.")
              continue

        elif question == "3":
          print(random.choice(list(self.facts2.values())))
          continue

        elif question == "4":
          print_slow("\nYou entered the white mansion...")
          time.sleep(1)
          self.white_mansion()
        

        elif question == "5":
          print("You go back...")
          return
          
        elif question == "inventory":
          print(self.inventory)
          self.hours += 0.05
          continue
        elif question == "time":
          print(f"{self.hours} hours")
          continue

      except:
        input("Incorrect, enter the number of your action.\nPress Enter to try again.")
        continue          


  def white_mansion(self):
    print_slow("\nSaleswoman: Hello, we're glad to see you!\n")
    print_slow("\nWHAT ARE YOU GOING TO DO? \n1. Build something \n2. Buy an animal \n3. Leave\n")
    while True:
      try:
        question = input("\nINPUT: ").strip()
        match question:
          case "1":
            print_slow("\nOUR CONSTRUCTION ASSORTMENT (write 4 to exit, choose the number of your choice.):")
            if self.hencoop_built:
              print_slow("\n1. CHICKEN COOP (PURCHASED)")
            else:
              print_slow("\n1. CHICKEN COOP")

            if self.cowshed_built:
              print_slow("\n2. COW SHED (PURCHASED)")
            else:
              print_slow("\n2. COW SHED")

            if self.sheepfold_built:
              print_slow("\n3. SHEEPFOLD (PURCHASED)")
            else:
              print_slow("\n3. SHEEPFOLD")

            if self.sheepfold_built and self.cowshed_built and self.hencoop:
              print_slow("\nStop! You've purchased everything!\n")
              continue

            else:
              print_slow("\nWHAT DO YOU WANT TO BUILD? (enter the choice number) 4 - if you want to exit.")
              while True:
                try:
                  question = input("\nINPUT: ")
                  match question:
                    case "1":
                      if self.hencoop_built:
                        print_slow("\nYou already have a chicken coop...")
                      else:
                        print_slow("\nSaleswoman: An ideal choice, the purchase will cost 450 coins...\n")
                        print_slow("DO YOU AGREE TO THE PURCHASE? yes/no")
                        while True:
                          try:
                            question = input("\nINPUT: ")
                            match question:
                              case "yes":
                                print_slow("PROCESSING...")
                                if self.money >= 450:
                                  print_slow("\nPurchased!")
                                  self.money -= 450
                                  print_slow("\nSaleswoman: we make preparations and then quickly install them on site, where chickens can eat naturally searching for food, and next to your house, we use trucks to transport the preparations! eco-friendly fuel...\n")
                                  time.sleep(3)
                                  self.hencoop_built = True
                                  self.process5 = True
                                  print_slow("\nWHAT DO YOU WANT TO BUILD? (enter the choice number) 4 - if you want to exit.")
                                  break

                              case "no":
                                print_slow("\nWHAT DO YOU WANT TO BUILD? (enter the choice number) 4 - if you want to exit.")
                                break

                              case "inventory":
                                print(self.inventory)
                                self.hours += 0.05
                                continue
                              case "time":
                                print(f"{self.hours} hours")
                                continue

                          except:
                            input("Incorrect, enter yes or no depending on your choice.\nPress Enter to try again.")
                            
                            
                    case "2":
                      if self.cowshed_built:
                        print_slow("\nYou already have a cow shed...")
                      else:
                        print_slow("\nSaleswoman: An expert's choice! the purchase will cost 900 coins...\n")
                        print_slow("DO YOU AGREE TO THE PURCHASE? yes/no")
                        while True:
                          try:
                            question = input("\nINPUT: ")
                            match question:
                              case "yes":
                                print_slow("PROCESSING...")
                                if self.money >= 900:
                                  print_slow("\nPurchased!")
                                  self.money -= 900
                                  print_slow("\nSaleswoman: we make preparations and then quickly install them on site, where cows can eat naturally searching for food, and next to your house, we use trucks to transport the preparations! eco-friendly fuel...\n")
                                  time.sleep(3)
                                  self.cowshed_built = True
                                  self.process6 = True
                                  print_slow("\nWHAT DO YOU WANT TO BUILD? (enter the choice number) 4 - if you want to exit.")
                                  break

                              case "no":
                                print_slow("\nWHAT DO YOU WANT TO BUILD? (enter the choice number) 4 - if you want to exit.")
                                break

                          except:
                            input("Incorrect, enter yes or no depending on your choice.\nPress Enter to try again.")
                            continue

                    case "3":
                      if self.sheepfold_built:
                        print_slow("\nYou already have a sheepfold...")
                      else:
                        print_slow("\nSaleswoman: You'll make a profit! the purchase will cost 800 coins...\n")
                        print_slow("DO YOU AGREE TO THE PURCHASE? yes/no")
                        while True:
                          try:
                            question = input("\nINPUT: ")
                            match question:
                              case "yes":
                                print_slow("PROCESSING...")
                                if self.money >= 800:
                                  print_slow("\nPurchased!")
                                  self.money -= 800
                                  print_slow("\nSaleswoman: we make preparations and then quickly install them on site, where sheep can eat naturally searching for food, and next to your house, we use trucks to transport the preparations! eco-friendly fuel...\n")
                                  time.sleep(3)
                                  self.sheepfold_built = True
                                  self.process7 = True
                                  print_slow("\nWHAT DO YOU WANT TO BUILD? (enter the choice number) 4 - if you want to exit.")
                                  break

                              case "no":
                                print_slow("\nWHAT DO YOU WANT TO BUILD? (enter the choice number) 4 - if you want to exit.")
                                break

                          except:
                            input("Incorrect, enter yes or no depending on your choice.\nPress Enter to try again.")
                            continue

                except:
                  input("Incorrect, enter the number of your action.\nPress Enter to try again.")
                  continue

          case "4":
                      return
          
          case "2":
            self.buy_animal()

          case "3":
            print_slow("YOU LEAVE...")
            return

      except:
        input("Incorrect, enter the number of your action.\nPress Enter to try again.")
        continue



  def floor_cave(self):
    if self.check_sleep:
      return
    print_slow("1 - MINE VARIOUS ORES, 2 - PLACE DYNAMITE, 3 - CHANGE PICKAXE, 4 - LEAVE. (give your answer as a number of your choice.)")
    while True:
      try:
        question = input("\nINPUT: ").capitalize().strip()
        if question == "1":
          self.mining()
        elif question == "2":
          self.dynamite_add()

        elif question == "3":
           
          pickaxe_choice = input("\nINPUT: ").strip()
          if pickaxe_choice == "1": 
            if self.has_item("Pickaxe"):
              self.pickaxe1 = False
              self.pickaxe2 = False
              self.pickaxe3 = False
              self.pickaxe4 = False
              self.pickaxe1 = True
              print("Selected: regular Pickaxe.")
            else:
              print_slow("You don't have a regular pickaxe... did you change the code?\n")
              continue

          elif pickaxe_choice == "2":
            if self.has_item("Aluminum Pickaxe"):
              self.pickaxe1 = False
              self.pickaxe2 = False
              self.pickaxe3 = False
              self.pickaxe4 = False
              self.pickaxe2 = True
              print("\nSelected: Aluminum Pickaxe.")
              break
            else:
              print_slow("You don't have an aluminum pickaxe...")
              time.sleep(1)
              continue

          elif pickaxe_choice == "3":
            if self.has_item("Iron Pickaxe"):
              self.pickaxe1 = False
              self.pickaxe2 = False
              self.pickaxe3 = False
              self.pickaxe4 = False
              self.pickaxe3 = True
              print("\nSelected: Iron Pickaxe.")
              break
            else:
              print_slow("You don't have an iron pickaxe...")
              time.sleep(1)
              continue

          elif pickaxe_choice == "4":
            if self.has_item("Steel Pickaxe"):
              self.pickaxe1 = False
              self.pickaxe2 = False
              self.pickaxe3 = False
              self.pickaxe4 = False
              self.pickaxe4 = True
              print("\nSelected: Steel Pickaxe.")
              break
            else:
              print_slow("You don't have a steel pickaxe...")
              time.sleep(1)
              continue

          elif question == "inventory":
            print(self.inventory)
            self.hours += 0.05
            continue
          elif question == "time":
            print(f"{self.hours} hours")
            continue
        
        elif question == "4":
          print_slow("YOU LEAVE...\n")
          return
        
        elif question == "inventory":
          print(self.inventory)
          self.hours += 0.05
          continue
        elif question == "time":
          print(f"{self.hours} hours")
          continue

      except:
        input("Incorrect, enter the number of your action.\nPress Enter to try again.")
        continue

  def mining(self):
    if self.check_sleep:
      return
    find = random.randint(1, 50)
    stones = random.randint(1, 10)
    iron = random.randint(1, 10)
    ruby = random.randint(1, 3)
    while True:
      try:
        if self.pickaxe1:
          self.mining_case += 1
          if self.mining_case == 5:
            print("YOU REACHED THE DESCENT DOWN, WRITE 1 - IF YOU WANT TO GO DOWN, 2 - IF YOU WANT TO LEAVE.")
            while True:
              try:
                question = input("\nINPUT: ").strip()
                if question == "1":
                  self.floor_up()
                  return

              except:
                input("Incorrect, enter the number of your action.\nPress Enter to try again.")
                continue

          self.hours += 0.3
          if 1 <= find <= 40:
            print(f"You found {stones} stones!")
            question = input("Pick up? yes/no \nINPUT: ").lower().strip()
            if question == "yes":
              self.add_inventory("Stone", stones)
            elif question == "no":
              print_slow("You didn't pick anything up...")

          elif 41 <= find <= 49:
            print(f"You found {iron} iron!")
            question = input("Pick up? yes/no \nINPUT: ").lower().strip()
            if question == "yes":
              self.add_inventory("Iron", iron)
            elif question == "no":
              print_slow("You didn't pick anything up...")

          elif find == 50:
            print(f"You found a rare item! {ruby} rubies!")
            question = input("Pick up? yes/no \nINPUT: ").lower().strip()
            if question == "yes":
              self.add_inventory("Ruby", ruby)
            elif question == "no":
              print_slow("You didn't pick anything up...")

        elif self.pickaxe2:
          self.hours += 0.3
          if 1 <= find <= 29:
            print(f"You found {stones} stones!")
            question = input("Pick up? yes/no \nINPUT: ").lower().strip()
            if question == "yes":
              self.add_inventory("Stone", stones)
            elif question == "no":
              print_slow("You didn't pick anything up...")

          elif 30 <= find <= 44:
            print(f"You found {iron} iron!")
            question = input("Pick up? yes/no \nINPUT: ").lower().strip()
            if question == "yes":
              self.add_inventory("Iron", iron)
            elif question == "no":
              print_slow("You didn't pick anything up...")

          elif 45 <= find <= 50:
            print(f"You found a rare item! {ruby} rubies!")
            question = input("Pick up? yes/no \nINPUT: ").lower().strip()
            if question == "yes":
              self.add_inventory("Ruby", ruby)
            elif question == "no":
              print_slow("You didn't pick anything up...")

        elif self.pickaxe3:
          self.hours += 0.3
          if 1 <= find <= 25:
            print(f"You found {stones} stones!")
            question = input("Pick up? yes/no \nINPUT: ").lower().strip()
            if question == "yes":
              self.add_inventory("Stone", stones)
            elif question == "no":
              print_slow("You didn't pick anything up...")

          elif 26 <= find <= 44:
            print(f"You found {iron} iron!")
            question = input("Pick up? yes/no \nINPUT: ").lower().strip()
            if question == "yes":
              self.add_inventory("Iron", iron)
            elif question == "no":
              print_slow("You didn't pick anything up...")

          elif 45 <= find <= 50:
            print(f"You found a rare item! {ruby} rubies!")
            question = input("Pick up? yes/no \nINPUT: ").lower().strip()
            if question == "yes":
              self.add_inventory("Ruby", ruby)
            elif question == "no":
              print_slow("You didn't pick anything up...")

        elif self.pickaxe4:
          self.hours += 0.3
          if 1 <= find <= 15:
            print(f"You found {stones} stones!")
            question = input("Pick up? yes/no \nINPUT: ").lower().strip()
            if question == "yes":
              self.add_inventory("Stone", stones)
            elif question == "no":
              print_slow("You didn't pick anything up...")

          elif 16 <= find <= 35:
            print(f"You found {iron} iron!")
            question = input("Pick up? yes/no \nINPUT: ").lower().strip()
            if question == "yes":
              self.add_inventory("Iron Ore", iron)
            elif question == "no":
              print_slow("You didn't pick anything up...")

          elif 36 <= find <= 50:
            print(f"You found a rare item! {ruby} rubies!")
            question = input("Pick up? yes/no \nINPUT: ").lower().strip()
            if question == "yes":
              self.add_inventory("Ruby", ruby)
            elif question == "no":
              print_slow("You didn't pick anything up...")

        exit_choice = input("CHOOSE ACTION: 1- LEAVE, 2 - CONTINUE.").strip()
        if exit_choice == "1":
          print_slow("YOU LEFT...")
          self.hours += 0.3
          return
        elif exit_choice == "2":
          continue

        elif question == "inventory":
          print(self.inventory)
          self.hours += 0.05
          continue
        elif question == "time":
          print(f"{self.hours} hours")
          continue

      except:
        input("Incorrect, enter yes or no depending on your choice.\nPress Enter to try again.")
        continue
    
  def dynamite_add(self):
    if self.has_item("Dynamite"):
      print_slow("ARE YOU SURE YOU WANT TO SPEND 1 DYNAMITE?... yes/no")
      while True:
        try:
          question = input("\nINPUT: ").lower().strip()
          if question == "yes":
            damage = random.randint(20, 45)
            self.health -= damage
            if self.health <= 0:
              print_slow(f"\nYou died from the explosion! you took {damage} damage... unfortunately you didn't have enough health. \n")
              input("Press Enter to return to the last saved game")
              self.load_game()
            print_slow("Dynamite... Sparks! BOOM...")
            find = random.randint(1, 25)
            stones = random.randint(3, 25)
            iron = random.randint(1, 10)
            ruby = random.randint(1, 5)
            if 1 <= find <= 20:
              print_slow(f"You got {stones} stones...")
              question = input("Pick up? yes/no \nINPUT: ").lower().strip()
              if question == "yes":
                self.add_inventory("Stone", stones)
              elif question == "no":
                print_slow("You didn't pick anything up...")
            
            elif 15 <= find <= 20:
              print_slow(f"You got {iron} iron...")
              question = input("Pick up? yes/no \nINPUT: ").lower().strip()
              if question == "yes":
                self.add_inventory("Iron Ore", iron)
              elif question == "no":
                print_slow("You didn't pick anything up...")

            elif 21 <= find <= 25:
              print_slow(f"You got {ruby} rubies! You're a lucky exploder..")
              question = input("Pick up? yes/no \nINPUT: ").lower().strip()
              if question == "yes":
                self.add_inventory("Ruby", ruby)
              elif question == "no":
                print_slow("You didn't pick anything up...")

            exit_choice = input(f"You took {damage} damage... you have {self.health} health left, risky!\nCHOICE (write the number of your choice): \n 1. Place more \n2. Leave")
            if exit_choice == "1":
              continue
            elif exit_choice == "2":
              print_slow("\nYou leave...")
              return
            
            elif question == "inventory":
              print(self.inventory)
              self.hours += 0.05
              continue
            elif question == "time":
              print(f"{self.hours} hours")
              continue

          elif question == "no":
            print_slow("\nYou leave...")
            return
          
          elif question == "inventory":
            print(self.inventory)
            self.hours += 0.05
            continue
          elif question == "time":
            print(f"{self.hours} hours")
            continue

        except:
          input("Incorrect, enter yes or no depending on your choice.\nPress Enter to try again.")
          continue

  def floor_up(self):
    self.mining_case = 0
    self.floor += 1
    if self.floor == 20:
      print_slow("You reached the end of the cave... ")
      self.add_inventory("Ruby", 8)
      input("Press Enter to exit here.")
      return
    if 15 <= self.floor <= 19:
      if self.battle == False:
        self.battle_start()
    
    print(f"FLOOR {self.floor}...")
    self.floor_cave()
  
  def rem_remains(self, item):
    if item in self.remains:
      del self.remains[item]
    if item in self.assortment:
      del self.assortment[item] 

  def add_remains(self, item, quantity=5):
    self.remains[item] = quantity
    self.assortment[item] = quantity

  def battle_start(self):
    print_slow("YOU WERE MET BY A STONE SLUG AT THE DESCENT...")
    self.enemy_health = 80
    while True:
      try:

        print_slow("WRITE 1 TO ATTACK.")
        attack = input("\nINPUT: ")
        if attack == "1":
          print("Punch...")
          enemy_damage = random.randint(1, 15)
          if self.health <= 0:
            print_slow(f"\nYou died from the slug! you took {enemy_damage} damage... unfortunately you didn't have enough health. \n")
            input("Press Enter to return to the last saved game")
            self.load_game()
          else:
            print_slow(f"The slug dealt you {enemy_damage} damage, painful!")
          
          if self.pickaxe1:
            damage = random.randint(15, 40)
          elif self.pickaxe2:
            damage = random.randint(25, 40)
          elif self.pickaxe3:
            damage = random.randint(35, 40)
          elif self.pickaxe4:
            damage = 40         
          self.enemy_health -= damage
          print_slow(f"You dealt {damage} damage to the enemy, he has {self.enemy_health} hp left.")
          print_slow("\nEnemy's turn.")
          time.sleep(0.05)
          print_slow("\nPunch...")

          if self.enemy_health <= 0:
            print("The slug is defeated! It will appear every time you go down...")
            self.battle = True
            return
          else:
            continue
          
      except: 
        input("\nIncorrect, write 1 to start the battle\n press Enter to continue..")
        continue

    

  def home(self):
    if self.check_sleep():
      return
    print_slow("\n\nCHOOSE ACTION NUMBER: \n", 0.04)
    print_slow("\n1. GO OUTSIDE\n\n2. SLEEP\n\n 3. OPEN CHEST ", 0.02)
    while True:
      try:
        question = input("\nINPUT: ").lower().strip()
        if question == "1":
          print("You went outside...")
          self.hours += 0.05
          return
        elif question == "2":
          while True:
            try:
              if self.hours < 18:
                print("Too early, if you want to fast forward to evening and sleep write 1, to get out of bed - 2.")
                question = input("INPUT: ").lower().strip()
                if question == "1":
                  self.hours = 19
                  print("Fast forwarded. Evening. You can sleep")
                  self.new_day()
                  break
                elif question == "inventory":
                  print(self.inventory)
                  self.hours += 0.05
                  continue
                elif question == "time":
                  print(f"{self.hours} hours")
                  continue
                else:
                  print("Going back.")
                  break
            
              else:
                print("After a while, you fell asleep...")
                self.new_day()
                break

            except:
              input("Incorrect, enter the number of your action.\nPress Enter to try again.")
              continue

        elif question == "3":
          self.hours += 0.05
          self.chest_open()

        elif question == "inventory":
          print(self.inventory)
          continue
        elif question == "time":
          print(f"{self.hours} hours")

      except:
        input("Incorrect, enter the number of your action.\nPress Enter to try again.")
        continue


  def add_chest(self, item, quantity=1):
    for cell in self.chest:
      if cell["name"] == item:
        cell["quantity"] += quantity
        print_slow(f"{item} now {cell['quantity']} pcs.", 0.03)
        return
    self.chest.append({"name": item, "quantity": quantity})
    print_slow(f"{item} added to chest. {quantity} pcs.", 0.03)

  def add_plant(self, item, quantity=1):
    for garden in self.garden:
      if garden["name"] == item:
        garden["quantity"] += quantity
        print_slow(f"{item} now {garden['quantity']} plants.", 0.03)
        return
    self.garden.append({"name": item, "quantity": quantity, "day": self.day})
    print_slow(f"{item} added to garden. {quantity} plants.", 0.03)

  def buy_animal(self):
    if self.check_sleep():
      return
    print_slow("WHICH ANIMAL DO YOU WANT TO BUY? \n1.CHICKENS \n2.COWS \n3. SHEEP  (4 - to exit)\n", 0.01)
    while True:
      try:
        question = input("\nINPUT: ").lower().strip()
        if question == "1":
          if self.hencoop_built == False:
            print_slow("\nFirst you need to get a chicken coop. Buy it from us.\n", 0.01)
          else:
            print_slow("\nONE CHICKEN COSTS 40$", 0.05)
            chickens_for_sale = random.randint(1, 8)
            print_slow(f"WE HAVE FOR SALE TODAY: {chickens_for_sale} CHICKENS.\n", 0.01)
            chicken_quantity = int(input("\nINPUT: "))
            if chicken_quantity > chickens_for_sale:
              print_slow(f"Sorry, but we only have {chickens_for_sale} chickens.", 0.01)
            else:
              total_price = chicken_quantity * 40
              print_slow(f"TOTAL PRICE: {total_price}$\n")
              print_slow("PROCESSING... \n", 0.005)
              time.sleep(1)
              
              if total_price >= self.money:
                print(f"\nYOU DON'T HAVE ENOUGH MONEY. NEEDS {total_price}$\n")
                continue
              else:
                self.hours += 0.25
                print_slow("\nPURCHASED. CHICKENS DELIVERED.\n")
                self.add_chicken("Chicken", chicken_quantity)
                self.money -= total_price
                self.chicken_count += chicken_quantity
                print(f"\nYou have {self.money}$ left")
                
                break

        elif question == "2":
          if self.cowshed_built == False:
            print_slow("\nFirst you need to get a cow shed. Buy it from us.\n", 0.01)
          else:
            print_slow("\nONE COW COSTS 120$", 0.05)
            cows_for_sale = random.randint(1, 5)
            print_slow(f"WE HAVE FOR SALE TODAY: {cows_for_sale} COWS.\n", 0.01)
            cow_quantity = int(input("\nINPUT: "))
            if cow_quantity > cows_for_sale:
              print_slow(f"Sorry, but we only have {cows_for_sale} cows.", 0.01)
            else:
              total_price = cow_quantity * 120
              print_slow(f"TOTAL PRICE: {total_price}$\n")
              print_slow("PROCESSING... \n", 0.005)
              time.sleep(1)
              
              if total_price >= self.money:
                print(f"\nYOU DON'T HAVE ENOUGH MONEY. NEEDS {total_price}$\n")
                continue
              else:
                self.hours += 0.25
                print_slow("\nPURCHASED. COWS DELIVERED.\n")
                self.add_cow("Cow", cow_quantity)
                self.money -= total_price
                self.cow_count += cow_quantity
                print(f"\nYou have {self.money}$ left")
                
                break
              
        elif question == "3":
          if self.sheepfold_built == False:
            print_slow("\nFirst you need to get a sheepfold. Buy it from us.\n", 0.01)
          else:
            print_slow("\nONE SHEEP COSTS 80$", 0.05)
            sheep_for_sale = random.randint(1, 5)
            print_slow(f"WE HAVE FOR SALE TODAY: {sheep_for_sale} SHEEP.\n", 0.01)
            sheep_quantity = int(input("\nINPUT: "))
            if sheep_quantity > sheep_for_sale:
              print_slow(f"Sorry, but we only have {sheep_for_sale} sheep.", 0.01)
            else:
              total_price = sheep_quantity * 80
              print_slow(f"TOTAL PRICE: {total_price}$\n")
              print_slow("PROCESSING... \n", 0.005)
              time.sleep(1)
              
              if total_price >= self.money:
                print(f"\nYOU DON'T HAVE ENOUGH MONEY. NEEDS {total_price}$\n")
                continue
              else:
                self.hours += 0.25
                print_slow("\nPURCHASED. SHEEP DELIVERED.\n")
                self.add_sheep("Sheep", sheep_quantity)
                self.money -= total_price
                self.sheep_count += sheep_quantity
                print(f"\nYou have {self.money}$ left")
                
                break

        elif question == "4":
          print_slow("\nWHAT ARE YOU GOING TO DO? \n1. Build something \n2. Buy an animal \n3. Leave\n")
          return
        

      except:
        input("Incorrect, enter the number of your choice for purchase.\nPress Enter to try again.")
        continue

  def buildings(self):
    if self.hencoop_built == True:
      print_slow("\n1. Chicken Coop", 0.07)
    else:
      print_slow("\n1. Chicken Coop (missing)", 0.07)
    if self.cowshed_built == True:
      print_slow("\n2. Cow Shed", 0.07)
    else:
      print_slow("\n2. Cow Shed (missing)", 0.07)
    if self.sheepfold_built == True:
      print_slow("\n3. Sheepfold")
    else:
      print_slow("\n3. Sheepfold (missing)")


    print_slow("\nWHERE DO YOU WANT TO ENTER? \nWRITE 4 IF YOU WANT TO EXIT.", 0.01)
    while True:
      try:
        question = input("\nINPUT: ").lower().strip()
        if question == "1":
          if self.hencoop_built == False:
            print_slow("You don't have a chicken coop yet...")
            continue
          else:
            self.hours += 0.25
            self.hencoop_go()

        elif question == "2":
          if self.cowshed_built == False:
            print_slow("You don't have a cow shed yet...")
            continue
          else:
            self.hours += 0.25
            self.cowshed_go()

        elif question == "3":
          if self.sheepfold_built == False:
            print_slow("You don't have a sheepfold yet...")
            continue
          else:
            self.hours += 0.25
            self.sheepfold_go()

        elif question == "4":
          print("You left...")
          return

        elif question == "inventory":
          print(self.inventory)
          self.hours += 0.05
          continue

        elif question == "time":
          print(f"{self.hours} hours")
          continue
      
      except:
        input("Incorrect, enter the number of your action.\nPress Enter to try again.")
        continue


  def add_chicken(self, animal, quantity=1):
    if self.hencoop_built:
        if animal in self.hencoop:
          self.hencoop[animal] += quantity
        else:
          self.hencoop[animal] = quantity
        print(f"{animal} now {self.hencoop[animal]} pcs.")

    else:
      print_slow("You don't have a chicken coop.")


  def add_cow(self, animal, quantity=1):
    if self.cowshed_built:
        if animal in self.cowshed:
          self.cowshed[animal] += quantity
        else:
          self.cowshed[animal] = quantity
        print(f"{animal} now {self.cowshed[animal]} pcs.")
    
    else:
      print_slow("You don't have a cow shed.")
      return


  def add_sheep(self, animal, quantity=1):
    if self.sheepfold_built:
        if animal in self.sheepfold:
          self.sheepfold[animal] += quantity
        else:
          self.sheepfold[animal] = quantity
        print(f"{animal} now {self.sheepfold[animal]} pcs.")

    else:
      print_slow("You don't have a sheepfold")


  def hencoop_go(self):
    print_slow("\nWELCOME TO YOUR CHICKEN COOP:\n")
    for bird, quantity in self.hencoop.items():
      print_slow(f"\n{bird} - {quantity} pcs.", 0.01)

    print_slow("\nChicken Coop\n\nWHAT ARE YOU GOING TO DO? \n1. CHECK NESTS \n2. CHECK BARREL \n3. LEAVE")
    while True:
      try:
        question = input("INPUT: ").lower().strip()
        if question == "1":
          self.hours += 0.15
          self.eggs_check()
        elif question == "2":
          self.hours += 0.15
          self.barrel_check()
        elif question == "3":
          print_slow("\nYOU LEAVE...")
          return

      except:
        input("Incorrect, enter the number of your action.\nPress Enter to try again.")
        continue


  def cowshed_go(self):
    print_slow("\nWELCOME TO YOUR COW SHED:\n")
    for cow, quantity in self.cowshed.items():
      print_slow(f"\n{cow} - {quantity} pcs.", 0.01)

    print_slow("\nCow Shed\n\nWHAT ARE YOU GOING TO DO? \n1. CHECK MILK AVAILABILITY FROM COWS \n2. LEAVE")
    while True:
      try:
        question = input("INPUT: ").lower().strip()
        if question == "1":
          self.hours += 0.15
          self.milk_check()
        elif question == "2":
          self.hours += 0.15
          return

      except:
        input("Incorrect, enter the number of your action.\nPress Enter to try again.")
        continue

  def sheepfold_go(self):
    print_slow("\nWELCOME TO YOUR SHEEPFOLD:\n")
    for sheep, quantity in self.sheepfold.items():
      print_slow(f"\n{sheep} - {quantity} pcs.", 0.01)

    print_slow("\nSheepfold\n\nWHAT ARE YOU GOING TO DO? \n1. CHECK WOOL AVAILABILITY FROM SHEEP \n2. LEAVE")
    while True:
      try:
        question = input("INPUT: ").lower().strip()
        if question == "1":
          self.hours += 0.15
          self.wool_check()
        elif question == "2":
          self.hours += 0.15
          return

      except:
        input("Incorrect, enter the number of your action.\nPress Enter to try again.")
        continue

  def milk_check(self):
    if self.milk_on == 0:
      print_slow("Milk hasn't appeared from the cows yet...")

    else:
      print_slow(f"\nThere is milk! {self.milk_on} liters. \nWrite 1 - to collect, 2 - to leave (Why!?) ")
      while True:
        try:
          question = input("\nINPUT: ").strip()
          if question == "1":
            print(f"Collected! {self.milk_on} liters of milk in bottles!")
            self.add_inventory("Milk", self.milk_on)
            self.milk_on = 0
            return

          elif question == "2":
            print_slow("You left...")
            return
          
          elif question == "inventory":
            print(self.inventory)
            self.hours += 0.05
            continue
          elif question == "time":
            print(f"{self.hours} hours")
            continue
        
        except:
          input("Incorrect, enter the number of your action.\nPress Enter to try again.")
          continue




  def wool_check(self):
    if self.wool_on == 0:
      print_slow("Your sheep are bald or haven't grown enough yet...")

    else:
      print_slow(f"\nThere is wool! {self.wool_on} pieces. \nWrite 1 - to collect, 2 - to leave (Why!?) ")
      while True:
        try:
          question = input("\nINPUT: ").strip()
          if question == "1":
            print(f"Collected! {self.wool_on} pieces of wool!")
            self.add_inventory("Wool", self.wool_on)
            self.wool_on = 0
            return

          elif question == "2":
            print_slow("You left...")
            return
          
          elif question == "inventory":
            print(self.inventory)
            self.hours += 0.05
            continue
          elif question == "time":
            print(f"{self.hours} hours")
            continue
        
        except:
          input("Incorrect, enter the number of your action.\nPress Enter to try again.")
          continue

  def eggs_check(self):
    if self.eggs_on == 0:
      print_slow("The chickens haven't laid eggs yet...")

    else:
      print_slow(f"\nThere are eggs! {self.eggs_on} chicken eggs. \nWrite 1 - to collect, 2 - to leave (Why!?) ")
      while True:
        try:
          question = input("\nINPUT: ").strip()
          if question == "1":
            print(f"Collected! {self.eggs_on} chicken eggs!")
            self.add_inventory("Egg", self.eggs_on)
            self.eggs_on = 0
            return

          elif question == "2":
            print_slow("You left...")
            return
          
          elif question == "inventory":
            print(self.inventory)
            self.hours += 0.05
            continue
          elif question == "time":
            print(f"{self.hours} hours")
            continue
        
        except:
          input("Incorrect, enter the number of your action.\nPress Enter to try again.")
          continue

  def barrel_check(self):
    print("You approached a small barrel with a small board attached...")
    if self.process1 == False and self.process2 == False and self.process3 == False and self.process4 == False:
      print_slow("\nThe barrel is empty...\nCHOICE: \n1. Put an egg \n2. Pour milk \n3. Pour milk and starter \n4. Pour milk and sour cream \n5. Leave")
      while True:
        try:
          question = input("INPUT: ").lower().strip()
          if question == "1":
            for cell in self.inventory:
              if cell["name"] == "Egg":
                self.take_inventory("Egg")
                print("You broke the egg into the board and mixed...")
                self.process1 = True
                return

              else:
                print_slow("\nYou don't have a chicken egg in your inventory.\n")
                time.sleep(1)
                continue

          elif question == "2":
            for cell in self.inventory:
              if cell["name"] == "Milk":
                self.take_inventory("Milk")
                print("You poured milk into the small barrel...")
                self.process2 = True
                return

              else:
                print_slow("\nYou don't have a bottle of milk in your inventory.\n")
                time.sleep(1)
                continue

          elif question == "3":
            self.ingredient_milk = False
            self.ingredient_sourdough = False
            for cell in self.inventory:
              if cell["name"] == "Milk":
                self.ingredient_milk = True
              if cell["name"] == "Starter":
                self.ingredient_sourdough = True

              if self.ingredient_milk and self.ingredient_sourdough:
                self.take_inventory("Milk")
                self.take_inventory("Starter")
                print("You poured milk and starter into the small barrel...")
                self.process3 = True
                return

              else:
                print_slow("\nYou don't have enough ingredients to make sour cream. Starter can be bought at the restaurant.\n")
                time.sleep(1)
                continue

          elif question == "4":
            self.ingredient_milk = False
            self.ingredient_sour_cream = False
            for cell in self.inventory:
              if cell["name"] == "Milk": 
                self.ingredient_milk = True
              if cell["name"] == "Sour Cream":
                self.ingredient_sour_cream = True

              if self.ingredient_milk and self.ingredient_sour_cream:
                self.take_inventory("Milk")
                self.take_inventory("Sour Cream")
                print("You poured milk into the board and added sour cream...")
                self.process4 = True
                return

              else:
                print_slow("\nYou don't have enough ingredients to make cottage cheese.\n")
                time.sleep(1)
                continue

          elif question == "5":
            return
          
          elif question == "inventory":
            print(self.inventory)
            self.hours += 0.05
            continue
          elif question == "time":
            print(f"{self.hours} hours")
            continue


        except:
          input("Incorrect, enter the number of your action.\nPress Enter to try again.")
          continue

    else:
      if self.process1:
        print_slow("Mayonnaise is still being prepared...")
        time.sleep(1)
        return
      elif self.process2:
        print_slow("Cheese is still being prepared...")
        time.sleep(1)
        return
      elif self.process3:
        print_slow("Sour cream is still being prepared...")
        time.sleep(1)
        return
      elif self.process4:
        print_slow("Cottage cheese is still being prepared...")
        time.sleep(1)
        return
      
      if self.mayonnaise == True:
        while True:
          try:
            question = input("Mayonnaise is ready. write 1 - to collect \n 2 - to leave (strange choice). \nINPUT: ")
            if question == "1":
              print_slow("Collected...")
              self.add_inventory("Mayonnaise")
              self.mayonnaise = False

            elif question == "2":
              print("You stepped away from the barrel with the board...")
              return
            
            elif question == "inventory":
              print(self.inventory)
              self.hours += 0.05
              continue

            elif question == "time":
              print(f"{self.hours} hours")
              continue

          except:
            input("Incorrect, enter the number of your action.\nPress Enter and try again.")
            break
            
          

      
      elif self.cheese == True:
        while True:
          try:
            question = input("Cheese is ready. write 1 - to collect \n 2 - to leave (strange choice). \nINPUT: ")
            if question == "1":
              print_slow("Collected...")
              self.add_inventory("Cheese")
              self.cheese = False

            elif question == "2":
              print("You stepped away from the barrel with the board...")
              return
            
            elif question == "inventory":
              print(self.inventory)
              self.hours += 0.05
              continue

            elif question == "time":
              print(f"{self.hours} hours")
              continue
            
          except:
            input("Incorrect, enter the number of your action.\nPress Enter and try again.")
            break

      elif self.sour_cream == True:
        while True:
          try:
            question = input("Sour cream is ready. write 1 - to collect \n 2 - to leave (strange choice). \nINPUT: ")
            if question == "1":
              print_slow("Collected...")
              self.add_inventory("Sour Cream")
              self.sour_cream = False

            elif question == "2":
              print("You stepped away from the barrel with the board...")
              return
            
          except:
            input("Incorrect, enter the number of your action.\nPress Enter and try again.")
            break

      elif self.curd == True:
        while True:
          try:
            question = input("Cottage cheese is ready. write 1 - to collect \n 2 - to leave (strange choice). \nINPUT: ")
            if question == "1":
              print_slow("Collected...")
              self.add_inventory("Cottage Cheese")
              self.curd = False

            elif question == "2":
              print("You stepped away from the barrel with the board...")
              return
            
            elif question == "inventory":
              print(self.inventory)
              self.hours += 0.05
              continue
            elif question == "time":
              print(f"{self.hours} hours")
              continue
            
          except:
            input("Incorrect, enter the number of your action.\nPress Enter and try again.")
            break

      
  def garden_show(self):
    print_slow("GARDEN:")
    if not self.garden:
      print_slow("garden beds are empty...", 0.03)
    for item in self.garden:
      print(f"{item['name']} - {item['quantity']} plants.")

  def garden_open(self):
    if self.check_sleep():
      return
    if self.winter == False:
      if not self.clear:
        print_slow("Everything is overgrown...", 0.04)
        while True:
          question = input("\nWrite 1 to remove weeds and start tending, 2 - if you want to go back... \nINPUT: ").lower().strip()
          if question == "1":
            print_slow("\nYou mowed everything. Continue mowing every 3 days.", 0.03)
            self.hours += 1
            self.clear = True
            self.ignore = 0
            self.garden_loop()
          elif question == "2":
            print("\nGoing back.")
            return
          elif question == "inventory":
            print(self.inventory)
            self.hours += 0.05
            continue
          elif question == "time":
            print(f"{self.hours} hours")
            continue

      print_slow("Welcome to your garden: ")
      self.garden_show()
      self.garden_loop()

    else:
      print_slow("Unfortunately it's winter and the garden is unavailable...")
      self.height = False

  def take_garden(self, item, quantity=1):
    for garden in self.garden[:]:
      if garden["name"] == item:
        if garden["quantity"] < quantity:
          print_slow("Not enough items.", 0.04)
          return False
        
        garden["quantity"] -= quantity
        print(f"Removed {quantity} {item}")

        if garden["quantity"] == 0:
          self.garden.remove(garden)

        
        return True
      
    print_slow(f"{item} not in inventory", 0.03)
    return False

  def garden_loop(self):
    if self.check_sleep():
      return
    while True:
      try:
        print_slow("Write\n 1 - if you want to leave\n 2 - if you want to add a plant\n 3 - if you want to remove a plant\n 4 - if you want to water the garden\n 5 - if you want to add fertilizer.", 0.005)
        question = input("\nINPUT: ")
        if question == "1":
          self.loop()
          return
        elif question == "2":
          question = input("WHAT FROM INVENTORY DO YOU WANT TO PLANT (example: Pumpkin Seeds)? 3 - if you want to exit. \nINPUT: ").lower().strip()
          print("Plowed earth...")
          if not any(item["name"].lower() == question.lower() for item in self.inventory):
            print("That's not in the inventory.")
            return
          self.add_plant(question)
          print("\n")
          self.garden_show()
          self.hours += 0.2
          continue
        elif question == "3":
          question = input("WHAT FROM THE GARDEN DO YOU WANT TO REMOVE? 3 - if you want to exit. \nINPUT: ").lower().strip()
          if question == "3":
            if not self.garden:
              print("Garden is empty.")
              continue
            return
          elif question == "inventory":
            print(self.inventory)
            self.hours += 0.02
            continue
          elif question == "time":
            print(f"{self.hours} hours")
            continue

          self.take_garden(question)
          print("\n")
          self.garden_show()
          self.hours += 0.2
          continue

        elif question == "4":
          if self.water == False:
            print_slow("\n\nYou don't have water in the watering can.\nThere's a small stream nearby! write 1 - if you want to get water from the stream\n2 - if you're going to leave.\n", 0.01)
            while True:
              try:
                question = input("\nINPUT: ").lower().strip()
                if question == "1":
                  print_slow("You go to the stream...", 0.01)
                  time.sleep(1)
                  print("A beautiful stream...")
                  time.sleep(0.08)
                  print_slow("\nYou filled the watering can..\n")
                  self.hours += 1
                  self.water = True
                  break
                elif question == "2":
                  print("\nYou left...")
                  return
                
                elif question == "inventory":
                  print(self.inventory)
                  self.hours += 0.05
                  continue

                elif question == "time":
                  print(f"{self.hours} hours")
                  continue
                
              except:
                input("Incorrect, enter the number of your action.\nPress Enter to try again.")
                continue
            
          else:
            if self.height == False:
              print("Unfortunately your plants have already dried up!")
              self.garden.clear()
            else:

              print_slow("\nYou watered the garden.")

            self.hours += 0.5
            self.watering = True
            self.watering_ignore = 0 
            self.water = False
            self.height = True
            time.sleep(1)
            continue
                
        elif question == "5":
          if "Fertilizer" not in self.inventory:
            print_slow("\n\nYou don't have fertilizer!\n", 0.01)
            continue
          else:
            print_slow("\n\nYou fertilized the garden... -5 days for plant growth.")
            self.take_inventory("Fertilizer", 1)
            self.hours += 0.5
            for plant in self.garden:
              plant["day"] -= 5
            time.sleep(1)
            continue

        elif question == "inventory":
          print(self.inventory)
          self.hours += 0.05
          continue
        elif question == "time":
          print(f"{self.hours} hours")
          continue
      except:
        
        continue


  def growing(self):
    if self.check_sleep():
      return
    if self.check_drought():
      return
    print("\n")
    for plant in self.garden[:]:
      grow_day = self.plant_growth[plant["name"]]
      if self.day - plant["day"] >= grow_day:
        print_slow(f"Plant {plant['name']} has grown")
        print("Write 1 - to harvest the plant, 2 - to leave (but why?...).")
        while True:
          try:
            question =  input("INPUT: ").lower().strip()
            if question == "1":
              print("Harvested...")
              self.hours += 0.1
              self.add_inventory(plant['name'])
              self.garden.remove(plant)
            elif question == "2":
              print("You left...")
              self.hours += 0.1
              return

          except:
            print("Incorrect, please write the number of your choice.")
            input("Press Enter to try again.")
            continue

      else:
        print_slow(f"Plant {plant['name']} is still growing...")
    
    
  def check_drought(self):
    if self.height == False:
      if self.garden:
        print_slow("\nUnfortunately your garden has dried up, water your garden every day! \nClearing...")
        self.garden.clear()
      return True
    return False
  

  def take_chest(self, item, quantity=1):
    for cell in self.chest[:]:
      if cell["name"] == item:
        if cell["quantity"] < quantity:
          print_slow("Not enough items.", 0.04)
          return False
        
        cell["quantity"] -= quantity
        print(f"Taken {quantity} {item}")

        if cell["quantity"] == 0:
          self.chest.remove(cell)



        return True
      
    print_slow(f"{item} not in chest", 0.03)
    return False
  
  def fast_menu(self):
    print("QUICK MENU: ")
    print_slow("\n\n1. SAVE GAME", 0.02)
    print_slow("\n2. LOAD GAME", 0.02)
    print_slow("\n3. INSTRUCTIONS", 0.02)
    print_slow("\n4. RESUME GAME", 0.02)
    while True:
      try:
        print_slow("What did you choose?")
        question = input("INPUT: ")
        if question == "1":
          print_slow("ARE YOU SURE? YES/NO:", 0.02)
          while True:
            try:
              question = input("INPUT: ").lower().strip()
              if question == "yes":
                print_slow("SAVED", 0.02)
                self.save_game()
                return
                  
              elif question == "no":
                print_slow("GOING BACK...")
                return
              
              elif question == "inventory":
                print(self.inventory)
                self.hours += 0.05
                continue
              elif question == "time":
                print(f"{self.hours} hours")
                continue


            except:
              print_slow("Error.", 0.01)
              input("Press Enter to continue.")
              continue
        elif question == "2":
          print_slow("ARE YOU SURE? YES/NO:", 0.02)
          while True:
            try:
              question = input("INPUT: ").lower().strip()
              if question == "yes":
                print_slow("LOADED", 0.02)
                self.load_game()
                return
              
              elif question == "no":
                print_slow("GOING BACK...")
                return
              
              elif question == "inventory":
                print(self.inventory)
                self.hours += 0.05
                continue
              elif question == "time":
                print(f"{self.hours} hours")
                continue


            except:
              print_slow("Error.", 0.01)
              input("Press Enter to continue.")
              continue


        elif question == "3":
          print_slow("\nINSTRUCTIONS:\n\n", 0.05)
          print_slow("1. How to choose an action:\nFor example, there are actions: eat, drink, sleep \nActions are numbered (1/2/3), \nIf for example you want to choose the action 'eat' then write 1 in the input.\n", 0.01)
          print_slow("2. If you want to open the inventory, write 'inventory' in the input, there is also your wallet, to check the time write 'time', to open the menu write 'menu'\n", 0.01)
          print_slow("3. It is recommended to always save the game to avoid losing progress.\n", 0.01)
          print_slow("4. Everything is saved in JSON.\n", 0.01)
          print_slow("5. Sorry, but the game only takes into account male age! women are beautiful.\n", 0.01)
          print_slow("\n\nThat's it. Have fun playing! \n\n")
          time.sleep(1)
          continue

        elif question == "4":
          print_slow("RESUMING...")
          return

        elif question == "inventory":
          print(self.inventory)
          self.hours += 0.05
          continue
        elif question == "time":
          print(f"{self.hours} hours")
          continue
      
              
      
      except:
        print("ERROR.")
        input("Press Enter to try again.")
        continue

  def chest_open(self):
    self.hours += 0.1
    print_slow("CHEST:")
    if not self.chest:
      print_slow("empty")
    for item in self.chest:
      print(f"{item['name']} - {item['quantity']} pcs")


  def add_inventory(self, item, quantity=1):
    for cell in self.inventory:
      if cell["name"] == item:
        cell["quantity"] += quantity
        print_slow(f"{item} now {cell['quantity']} pcs.", 0.03)
        return
    self.inventory.append({"name": item, "quantity": quantity})
    print_slow(f"{item} added to inventory. {quantity} pcs.", 0.03)

  def take_inventory(self, item, quantity=1):
    no = ["Pickaxe", "Scythe", "Watering Can", "Aluminum Pickaxe", "Iron Pickaxe", "Steel Pickaxe"]
    if item in no:
      print("You can't throw this away")
      return False
    for cell in self.inventory[:]:
      if cell["name"] == item:
        if cell["quantity"] < quantity:
          print_slow("Not enough items.", 0.04)
          return False
        
        cell["quantity"] -= quantity
        print(f"Removed {quantity} {item}")

        if cell["quantity"] == 0:
          self.inventory.remove(cell)

        
        return True
      
    print_slow(f"{item} not in inventory", 0.03)
    return False

  def has_item(self, item):
    for cell in self.inventory:
      if cell["name"] == item:
        return True
    return False

  def inventory_open(self):
    print_slow("INVENTORY:")
    print(f"Your balance: {self.money}$")
    if not self.inventory:
      print_slow("empty")
    for item in self.inventory:
      print(f"{item['name']} - {item['quantity']} pcs")

  def check_sleep(self):
    if self.hours >= 24:
      print("You fell asleep right on the spot...")
      self.new_day()
      return True
    elif self.hours > 22:
      print("You're starting to fall asleep, go home quickly.")  
    return False
    

  def new_day(self):
    self.save_game()
    self.health = 100
    self.luck1 = True
    self.day += 1
    self.hours = 6
    self.ignore += 1
    self.watering = False
    self.watering_ignore += 1
    
    if self.summer == True:
      self.rem_remains("Wheat Seeds")
      self.rem_remains("Carrot Seeds")
      self.rem_remains("Cabbage Seeds")
      self.rem_remains("Beet Seeds")
      self.rem_remains("Cucumber Seeds")
      self.rem_remains("Corn Seeds")
      self.rem_remains("Tomato Seeds")
      self.rem_remains("Fertilizer")
      self.add_remains("Wheat Seeds", 5)
      self.add_remains("Carrot Seeds", 5)
      self.add_remains("Cabbage Seeds", 5)
      self.add_remains("Beet Seeds", 5)
      self.rem_remains("Pumpkin Seeds")
      self.add_remains("Cucumber Seeds", 5)
      self.add_remains("Corn Seeds", 5)
      self.add_remains("Tomato Seeds", 5)
      self.add_remains("Fertilizer", 5)
    elif self.autumn == True:
      self.rem_remains("Wheat Seeds")
      self.rem_remains("Cabbage Seeds")
      self.rem_remains("Pumpkin Seeds")
      self.rem_remains("Cucumber Seeds")
      self.rem_remains("Tomato Seeds")
      self.rem_remains("Fertilizer")
      self.add_remains("Wheat Seeds", 8)
      self.rem_remains("Carrot Seeds")
      self.add_remains("Cabbage Seeds", 3)
      self.rem_remains("Beet Seeds")
      self.add_remains("Pumpkin Seeds", 15)
      self.rem_remains("Cucumber Seeds")
      self.add_remains("Corn Seeds", 2)
      self.add_remains("Tomato Seeds", 4)
      self.add_remains("Fertilizer", 3)
    elif self.winter == True:
      self.rem_remains("Wheat Seeds")
      self.rem_remains("Carrot Seeds")
      self.rem_remains("Cabbage Seeds")
      self.rem_remains("Beet Seeds")
      self.rem_remains("Pumpkin Seeds")
      self.rem_remains("Cucumber Seeds")
      self.rem_remains("Corn Seeds")
      self.rem_remains("Tomato Seeds")
      self.rem_remains("Fertilizer")
    elif self.spring == True:
      self.rem_remains("Wheat Seeds")
      self.rem_remains("Carrot Seeds")
      self.rem_remains("Cabbage Seeds")
      self.rem_remains("Beet Seeds")
      self.rem_remains("Cucumber Seeds")
      self.rem_remains("Corn Seeds")
      self.rem_remains("Tomato Seeds")
      self.rem_remains("Fertilizer")
      self.add_remains("Wheat Seeds", 10)
      self.add_remains("Carrot Seeds", 7)
      self.add_remains("Cabbage Seeds", 3)
      self.add_remains("Beet Seeds", 7)
      self.rem_remains("Pumpkin Seeds")
      self.add_remains("Cucumber Seeds", 7)
      self.add_remains("Corn Seeds", 10)
      self.add_remains("Tomato Seeds", 6)
      self.add_remains("Fertilizer", 10)

    if self.day == 5:
      if not self.gift_give_2:
        print_slow("NEW ITEM: Gift with a note...")
        print_slow("Hi. Nephew\nI'm giving you 500$... \nI recommend you buy a chicken coop with it\n But in the end it's up to you, you're the new owner of a big farm! \nI'm so glad you like living here\n\nYour Aunt Jael.")
        self.money += 500
        self.gift_give_2 = True

    if self.process1:
      self.record1 += 1
      if self.record1 == 2:
        self.process1 = False
        self.mayonnaise = True
        self.record1 = 0

    if self.process2:
      self.record2 += 1
      if self.record2 == 5:
        self.process2 = False
        self.cheese = True
        self.record2 = 0


    if self.process3:
      self.record3 += 1
      if self.record3 == 3:
        self.process3 = False
        self.sour_cream = True
        self.record3 = 0

    if self.process4:
      self.record4 += 1
      if self.record4 == 7:
        self.process4 = False
        self.curd = True
        self.record4 = 0

    if self.process5 and self.chicken_count != 0:       
        self.egg_production = 1 * self.chicken_count
        self.record5 += 1
        if self.record5 == 5:
          self.eggs_on += self.egg_production
          self.record5 = 0          
    else:
      pass

    if self.process6 and self.cow_count != 0:      
        self.milk_production = 1 * self.cow_count
        self.record6 += 1
        if self.record6 == 5:
          self.milk_on += self.milk_production
          self.record6 = 0          
    else:
      pass

    if self.process7 and self.sheep_count != 0:
        self.wool_production = 1 * self.sheep_count
        self.record7 += 1
        if self.record7 == 5:
          self.wool_on += self.wool_production
          self.record7 = 0         
    else:
      pass

    

    if self.watering_ignore == 5:
      self.height = False

    self.growing()
    
      

    print(f"DAY {self.day}\n")
    print_slow(f"{self.days[(self.day - 1) % 7]}\n", 0.08)
    weather = random.randint(1, 4)
    if weather == 2:
      self.watering = True
      self.watering_ignore = 0

    if self.day < 92:
      print_slow("SUMMER", 0.03)
      self.summer = True
      self.autumn = False
      self.winter = False
      self.spring = False
      if weather == 1:
        print("sunny...\n\n")
      elif weather == 2:
        print("rain...")
      elif weather == 3:
        print("storm...")
      else:
        print("fog...")
    elif self.day < 181:
      print_slow("AUTUMN", 0.03)
      self.autumn = True
      self.summer = False
      self.winter = False
      self.spring = False
      if weather == 1:
        print("sunny...\n\n")
      elif weather == 2:
        print("rain...")
      elif weather == 3:
        print("storm...")
      else:
        print("fog...")      
    elif self.day < 272:
      print_slow("WINTER", 0.03)
      self.winter = True
      self.summer = False
      self.autumn = False
      self.spring = False
      if weather == 1:
        print("sunny...\n\n")
      elif weather == 2:
        print("rain...")
      elif weather == 3:
        print("storm...")
      else:
        print("fog...")      
    elif self.day < 365:
      print_slow("SPRING", 0.03)
      self.spring = True
      self.summer = False
      self.autumn = False
      self.winter = False
      if weather == 1:
        print("sunny...\n\n")
      elif weather == 2:
        print("rain...")
      elif weather == 3:
        print("storm...")
      else:
        print("fog...")      
    elif self.day == 365:
      self.day = 0

    print_slow("\n\nPress any key and Enter to leave the house.", 0.03)
    input("INPUT: ")
    self.loop()

  def instructions(self):
    print_slow("\nINSTRUCTIONS:\n\n", 0.05)
    print_slow("1. How to choose an action:\nFor example, there are actions: eat, drink, sleep \nActions are numbered (1/2/3), \nIf for example you want to choose the action 'eat' then write 1 in the input.\n", 0.01)
    print_slow("2. If you want to open the inventory, write 'inventory' in the input, there is also your wallet, to check the time write 'time', to open the menu write 'menu'\n", 0.01)
    print_slow("3. It is recommended to always save the game to avoid losing progress.\n", 0.01)
    print_slow("4. Everything is saved in JSON.\n", 0.01)
    print_slow("5. Sorry, but the game only takes into account male age! women are beautiful.\n", 0.01)
    print_slow("\n\nThat's it. Have fun playing! \n\n")
    time.sleep(1)
    self.menu()

  
  def preservation(self):
    print_slow("\nSAVES:", 0.05)
    load = input("\nAre you sure you want to save to the last save? yes/no: ").lower().strip()
    if load == "yes":
      self.load_game()
    else:
      print("Going back...")
      time.sleep(2)
      self.menu()
      
  def load_game(self):
    try:
      with open("save.json", "r") as f:
        self.loaded = json.load(f)
        self.day = self.loaded["day"] 
        self.money = self.loaded["money"]
        self.inventory = self.loaded["inventory"]
        self.chest = self.loaded["chest"]
        self.garden = self.loaded["garden"]
        self.clear = self.loaded["clear"]
        self.ignore = self.loaded["ignore"]
        self.watering_ignore = self.loaded["watering_ignore"]
        self.hours = self.loaded["hours"]

        self.hencoop_built = self.loaded["hencoop_built"]
        self.hencoop = self.loaded["hencoop"]
        self.cowshed_built = self.loaded["cowshed_built"]
        self.cowshed = self.loaded["cowshed"]
        self.sheepfold_built = self.loaded["sheepfold_built"]
        self.sheepfold = self.loaded["sheepfold"]
        self.eggs_on = self.loaded["eggs"]
        self.milk_on = self.loaded["milk"]
        self.wool_on = self.loaded["wool"]        
        self.barrel = self.loaded["barrel"]
        self.gift_give_1 = self.loaded["gift_give_1"]
        self.gift_give_2 = self.loaded["gift_give_2"]
        self.process1 = self.loaded["process1"]
        self.process2 = self.loaded["process2"]
        self.process3 = self.loaded["process3"]
        self.process4 = self.loaded["process4"]
        self.record1 = self.loaded["record1"]
        self.record2 = self.loaded["record2"]
        self.record3 = self.loaded["record3"]
        self.record4 = self.loaded["record4"]
        self.mayonnaise = self.loaded["mayonnaise"]
        self.cheese = self.loaded["cheese"]
        self.sour_cream = self.loaded["sour_cream"]
        self.curd = self.loaded["curd"]
        self.ingredient_egg = self.loaded["ingredient_egg"]
        self.ingredient_milk = self.loaded["ingredient_milk"]
        self.ingredient_sourdough = self.loaded["ingredient_sourdough"]
        self.ingredient_sour_cream = self.loaded["ingredient_sour_cream"]
        self.dynamite_assortment = self.loaded["dynamite_assortment"]


        print(f"Continuing from day {self.day}")
        print_slow("...", 0.5)
        self.loop()
    except FileNotFoundError:
      print_slow("New game...", 0.1)
      self.game_start()

  def save_game(self):
    data = {
      "day": self.day,
      "money": self.money,
      "inventory": self.inventory,
      "chest": self.chest,
      "garden": self.garden,
      "clear": self.clear,
      "ignore": self.ignore,
      "watering_ignore": self.watering_ignore,
      "hours": self.hours,

      "hencoop_built": self.hencoop_built,
      "hencoop": self.hencoop,
      "cowshed_built": self.cowshed_built,
      "cowshed": self.cowshed,
      "sheepfold_built": self.sheepfold_built,
      "sheepfold": self.sheepfold,
      "eggs": self.eggs_on,
      "milk": self.milk_on,
      "wool": self.wool_on,
      "barrel": self.barrel,
      "gift_give_1": self.gift_give_1,
      "gift_give_2": self.gift_give_2,
      "process1": self.process1,
      "process2": self.process2,
      "process3": self.process3,
      "process4": self.process4,
      "record1": self.record1,
      "record2": self.record2,
      "record3": self.record3,
      "record4": self.record4,
      "mayonnaise": self.mayonnaise,
      "cheese": self.cheese,
      "sour_cream": self.sour_cream,
      "curd": self.curd,
      "ingredient_egg": self.ingredient_egg,
      "ingredient_milk": self.ingredient_milk,
      "ingredient_sourdough": self.ingredient_sourdough,
      "ingredient_sour_cream": self.ingredient_sour_cream,
      "dynamite_assortment": self.dynamite_assortment
    }
    with open("save.json", "w", encoding="utf-8") as f:
      json.dump(data, f, ensure_ascii=False, indent=4)
    print_slow("\nGame saved", 0.08)





game().menu()
