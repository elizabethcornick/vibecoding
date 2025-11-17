# vibecoding
Learn how to make a vibe coding journal


import ipywidgets as widgets
from IPython.display import display, HTML
from datetime import datetime

# Assuming coding_journal is initialized globally as `[]`
# If it's not, ensure it's defined: coding_journal = []

# Widget for mood selection
mood_selector = widgets.Dropdown(
    options=['Happy', 'Chill', 'Focused', 'Creative', 'Energetic', 'Frustrated', 'Learning'],
    value='Focused',
    description='Current Mood:',
    disabled=False,
)

# Widget for journal entry text
journal_input = widgets.Textarea(
    value='',
    placeholder='Write about your coding session...',    description='Journal Entry:',
    disabled=False
)

# Button to add entry
add_entry_button = widgets.Button(description='Add Journal Entry')

# Output widget to display the journal
journal_output = widgets.Output()

# Define mood styles
mood_styles = {
    'Happy': {'color': 'green', 'emoji': '😊'},
    'Chill': {'color': 'blue', 'emoji': '😌'},
    'Focused': {'color': 'purple', 'emoji': '🧠'},
    'Creative': {'color': 'orange', 'emoji': '🎨'},
    'Energetic': {'color': 'red', 'emoji': '⚡'},
    'Frustrated': {'color': 'darkred', 'emoji': '😩'},
    'Learning': {'color': 'darkgreen', 'emoji': '📚'}
}

def add_journal_entry(b):
    with journal_output:
        journal_output.clear_output()
        current_time = datetime.now().strftime('%Y-%m-%d %H:%M:%S')
        entry = {
            'timestamp': current_time,
            'mood': mood_selector.value,
            'entry': journal_input.value
        }
        coding_journal.append(entry)
        journal_input.value = '' # Clear input after adding

        display(HTML("<h3>--- Coding Journal ---</h3>"))
        for i, item in enumerate(coding_journal):
            mood_info = mood_styles.get(item['mood'], {'color': 'black', 'emoji': '💬'})
            color = mood_info['color']
            emoji = mood_info['emoji']
            html_string = f"<p style='color: {color};'>[{item['timestamp']}] Mood: {emoji} {item['mood']} - {item['entry']}</p>"
            display(HTML(html_string))
        display(HTML("<h3>----------------------</h3>"))

add_entry_button.on_click(add_journal_entry)

display(mood_selector, journal_input, add_entry_button, journal_output)
