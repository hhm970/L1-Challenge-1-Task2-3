# L1-Challenge-1-Task2-3

from random import randint
 
def reverse_name(name):
  # Reverses the characters of a given name
  return name[::-1]
  #Can also do the following:
  #result = ""
  #for letter in name:
  #  result = letter + result
  #return result

def intersperse(forename, surname):
  # Intersperses a surname with a reversed first name
  # As strings are immutable, we need to do this all in one go.
  result = ""
  len_f = len(forename)
  len_s = len(surname)
  # Establish which of the forename or surname is shorter,
  # and iterate around the lesser length n.
  n = min(len_f, len_s)
  # Note how the forename is reversed, but the surname is not.
  # We index characters from forename from the end of the string,
  # while characters from surname are indexed from the beginning.
  f_counter = len_f - 1
  s_counter = 0
  # Iterating; we want even indices to be of forename characters,
  # and odd indices to be of surname characters.
  # We iterate over the range of 2n to account for two iterands being used.
  for i in range(2 * n):
    if i % 2:
      result = result + surname[s_counter]
      s_counter +=1
    else:
      result = result + forename[f_counter]
      f_counter -= 1
  # For the longer of the forename/surname, we either add the remaining
  # characters of the surname, or the characters of the reversed forename.
  if len_f < len_s:
    result += surname[n:]
  elif len_s < len_f:
    result = result + reverse_name(forename[:n])
  return result

def format_name(name):
  n = len(name) // 2
  first_part = name[:n]
  second_part = name[n:]
  return first_part + " " + second_part

# OPTIONS MENU FOR CREATING USERNAME

print("Welcome to the username creator!")
print("Please choose one of the following options: ")
print("1. Create a username based on a name.")
print("2. Generate random username.")
choice = input("Enter choice: ")

if choice == "1":
  forename = input("Enter first name here: ")
  surname = input("Enter last name here: ")
  username = format_name(intersperse(forename, surname))
  print(f"Your username is: {username}")
elif choice == "2":
  name = ""
  while len(name) < 10:
    if randint(0, 1):
      name = str(randint(0, 9)) + name
    else:
      name = chr(randint(ord('a'), ord('z'))) + name
  username = format_name(name)
  print(f"Your username is {username}")
else:
  raise ValueError("You can only enter 1 or 2.")
