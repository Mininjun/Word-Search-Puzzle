# Word-Search-Puzzle
This is going to be a Word Puzzle Learning science with fun for your children.
import random
from typing import List

def create_crossword(words: List[str]) -> List[List[str]]:
    grid = [['.' for _ in range(10)] for _ in range(10)]
    directions = [
        (0, 1),   # right
        (1, 0),   # down
        (1, 1),   # down-right
        (1, -1),  # down-left
        (0, -1),  # left
        (-1, 0),  # up
        (-1, 1),  # up-right
        (-1, -1)  # up-left
    ]
    
    for word in words:
        word_upper = word.upper()
        placed = False
        for attempt in [word_upper, word_upper[::-1]]:
            if placed:
                break
            random.shuffle(directions)
            for dr, dc in directions:
                if placed:
                    break
                positions = [(r, c) for r in range(10) for c in range(10)]
                random.shuffle(positions)
                for r, c in positions:
                    length = len(attempt)
                    end_r = r + dr * (length - 1)
                    end_c = c + dc * (length - 1)
                    if end_r < 0 or end_r >= 10 or end_c < 0 or end_c >= 10:
                        continue
                    valid = True
                    for i in range(length):
                        nr, nc = r + i * dr, c + i * dc
                        if grid[nr][nc] != '.' and grid[nr][nc] != attempt[i]:
                            valid = False
                            break
                    if valid:
                        for i in range(length):
                            nr, nc = r + i * dr, c + i * dc
                            grid[nr][nc] = attempt[i]
                        placed = True
                        break
        if not placed:
            print(f"Warning: Could not place word '{word}'")
    
    letters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'
    for i in range(10):
        for j in range(10):
            if grid[i][j] == '.':
                grid[i][j] = random.choice(letters)
                
    return grid
