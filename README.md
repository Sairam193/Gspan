# Gspan

def split_into_lines(paragraph, page_width):
    words = paragraph.split()
    lines = []
    current_line = []

    for word in words:
        if sum(len(w) for w in current_line) + len(current_line) + len(word) <= page_width:
            current_line.append(word)
        else:
            lines.append(current_line)
            current_line = [word]

    lines.append(current_line)

    return lines



def justify_line(line, page_width):
    spaces_to_add = page_width - sum(len(word) for word in line)
    if len(line) > 1:
        spaces_between_words = spaces_to_add // (len(line) - 1)
        extra_spaces = spaces_to_add % (len(line) - 1)
        justified_line = (' ' * spaces_between_words).join(word + ' ' * (1 if i < extra_spaces else 0) for i, word in enumerate(line))
    else:
        justified_line = line[0].ljust(page_width)

    return justified_line


paragraph = "This is an sample text but a complecated problem to be solved, so we are adding more text to see that it actually works."
page_width = 20
lines_array = split_into_lines(paragraph, page_width)

for line in lines_array:
    justified_line = justify_line(line, page_width)
    print(justified_line)
