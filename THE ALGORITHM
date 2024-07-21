import matplotlib.pyplot as plt

print("How many rows are in the word search?")
numRows = int(input(">"))
print("How many collums are in the word search?")
numCol = int(input(">"))
wordSearch = []
for i in range(numRows):
  print("Please type a row of letters going from left to right, top to bottom.")
  row = input(">")
  row = list(row)
  wordSearch.append(row)

wordBank = []
print("How many word(s) are there to search for?")
numWords = int(input(">"))
for i in range(numWords):
  print("Please enter each word individually below.")
  wordBank.append(input(">"))

solutions = []

def search_word(word, current_letter_index, row, col, direction, path):
  global solutions
  path.append([row, col])
  if current_letter_index == len(word):
    solutions.append([path, direction])
    return

  next_row, next_col = row, col
  if direction == "down":
    next_row += 1
  elif direction == "up":
    next_row -= 1
  elif direction == "right":
    next_col += 1
  elif direction == "left":
    next_col -= 1

  if 0 <= next_row < numRows and 0 <= next_col < numCol and word[current_letter_index] == wordSearch[next_row][next_col]:
    search_word(word, current_letter_index + 1, next_row, next_col, direction, path.copy())

# Optimization: Only check for starting letters once per word
for word_index in range(len(wordBank)):
  word = wordBank[word_index]
  for row in range(numRows):
    for col in range(numCol):
      for letter_index in range(len(word)):  # Check for all starting letters
        if word[letter_index] == wordSearch[row][col]:
          # Check all directions from this starting point
          search_word(word, letter_index + 1, row, col, "down", [[row, col]])
          search_word(word, letter_index + 1, row, col, "up", [[row, col]])
          search_word(word, letter_index + 1, row, col, "right", [[row, col]])
          search_word(word, letter_index + 1, row, col, "left", [[row, col]])

# Visualization using matplotlib
fig, ax = plt.subplots()

# Create the grid
for row_index, row in enumerate(wordSearch):
  for col_index, letter in enumerate(row):
    ax.text(col_index, row_index, letter, ha='center', va='center')

# Highlight solutions
for solution in solutions:
  path, direction = solution
  for i in range(len(path) - 1):
    row1, col1 = path[i]
    row2, col2 = path[i + 1]
    if direction == "down":
      ax.plot([col1, col2], [row1, row2], 'ro-', linewidth=2)
    elif direction == "up":
      ax.plot([col1, col2], [row1, row2], 'go-', linewidth=2)
    elif direction == "right":
      ax.plot([col1, col2], [row1, row2], 'bo-', linewidth=2)
    elif direction == "left":
      ax.plot([col1, col2], [row1, row2], 'co-', linewidth=2)

ax.set_xlim(-1, numCol)
ax.set_ylim(-1, numRows)
ax.invert_yaxis()  # Make y-axis top-to-bottom
plt.show()
