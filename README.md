 import random 
MAX_LINES=3
MAX_BET =100
MIN_BET=10
ROWS=3
COLS=3
#the dictionary to store the symbol count
symbo_count={
   "A":2,
   "B":3,
   "C":5,
   "D":6
}

symbo_value={
   "A":6,
   "B":3,
   "C":2,
   "D":1
}
     
#the alogorithym for depositing money
def deposit():
 while True:
    amount=input("please enter a amount to deposit$ ")
    if amount.isdigit():
        amount=int(amount)
        if amount > 0:
            return amount
        else:
           print("please enter a digit greator then 0")
    else:
       print("please enter a valid digit ")
   
#the alogorythm for selcting lines 
def number_of_lines():
 
 while True:
    lines=input("please enter the number of lines(1-"+str(MAX_LINES)+")? ")

    if lines.isdigit():
        lines=int(lines)
        if 1<=lines<=MAX_LINES:
         return lines  
          
        else:
           print("please enter a valid number of lines")
    else:
       print("please enter a valid digit ")
    
#get the amount of bet on each line 
def get_bet():
   
   while True:
    amount=input("please enter a amount to bet on each line  ")
    if amount.isdigit():

        amount=int(amount)
        if MIN_BET<= amount <=MAX_BET:
            return amount
        else:
           print(f"amount must be between ${MIN_BET}-{MAX_BET}")
    else:
       print("please enter a valid digit ")

#the algorithym for spining the slot machine 



def get_slot_machine_spinning(rows,cols,symbols):
   all_sybols=[]
   for symbo,symbo_count in symbols.items():
      for _ in range(symbo_count):
         all_sybols.append(symbo)
 
   colomns=[] 
   for _ in range(cols):
      colmn=[]
      currnet_symbol=all_sybols[:]
      for _ in range(rows):
         value=random.choice(currnet_symbol)
         currnet_symbol.remove(value)
         colmn.append(value)
      colomns.append(colmn)
   return colomns   

#printng the slot machine algorithym


def print_slot_machine(colomns):
   for row in range(len(colomns[0])):
      for i , column in enumerate(colomns):
         if i != len(colomns) - 1:
            print(column[row], end="|")
         else:
            print(column[row], end="")   
      print()   

# alogrithym for winning

def user_winning(columns,lines,bet,value):
   winng=0
   winning_line =[]
   for line in range(lines):
      symbol=columns[0][line]
      for column in columns:
         symbol_check= column[line]
         if symbol!=symbol_check:
            break
         else:
            winng+=value[symbol]*bet
            winning_line.append(line+1)
   return winng,winning_line        


def main():
   balance= deposit()
   lines=number_of_lines()
   while True:  
    bet = get_bet()
    total_bet=lines*bet
    if total_bet > balance:
     print(f"you dont have enough balence your current balence is {balance}")
    else:
      
      break 
   print(f"you are betting {bet}on {lines} lines. your total bet is {total_bet} " ) 
   #printing slot machine 
   slots= get_slot_machine_spinning(ROWS,COLS,symbo_count)
   print_slot_machine(slots)
   winning,winning_line=user_winning(slots,lines,bet,symbo_value)
   print(f"you won $ {winning}.")
   print(f"you won on line:  ",*winning_line)


main() 

  

   
