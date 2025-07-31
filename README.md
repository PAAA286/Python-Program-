# Python-Program-
A simple personal assistant 

    
       import os
      import random
    from datetime import datetime

    def get_user_info():
    print("\nHello! I'm your simple personal assistant. Let's get to know each other.")
    questions = [
        {"prompt": "What's your name? ", "key": "Name"},
        {"prompt": "How old are you? ", "key": "Age"},
        {"prompt": "What's your favorite color? ", "key": "Favorite Color"},
        {"prompt": "What's your favorite food? ", "key": "Favorite Food"},
        {"prompt": "Which city do you live in? ", "key": "City"},
        {"prompt": "What's your favorite movie? ", "key": "Favorite Movie"},
        {"prompt": "Which soccer team do you support? ", "key": "Favorite Soccer Team"},
        {"prompt": "What's one of your favorite hobbies? ", "key": "Hobby"}
    ]
    random.shuffle(questions)

    user_data = {}
    for q_data in questions:
        answer = input(q_data["prompt"])
        user_data[q_data["key"]] = answer

    return user_data 
    def display_summary(user_data):
    print("\n--- Your Personal Summary ---")
    print(f"Hello, {user_data.get('Name', 'there')}!")
    print(f"At {user_data.get('Age', 'an unknown age')} years old, you love the color {user_data.get('Favorite Color', 'a mystery color')},")
    print(f"enjoy eating {user_data.get('Favorite Food', 'something delicious')}, and live in {user_data.get('City', 'an undisclosed city')}.")
    print(f"Life must be awesome watching {user_data.get('Favorite Movie', 'a great movie')},")
    print(f"and cheering for {user_data.get('Favorite Soccer Team', 'your favorite team')}!")
    print(f"It's great you enjoy {user_data.get('Hobby', 'many fun activities')} in your free time.")
    print("----------------------------")
    def save_to_file(user_data):
    while True:
        filename = input("Enter the full path and filename (e.g., C:/Users/YourName/summary.txt or summary.txt for current folder): ")
        if not filename:
            print("Filename cannot be empty. Please try again.")
            continue
        try:
            dir_name = os.path.dirname(filename)
            if dir_name and not os.path.exists(dir_name):
                os.makedirs(dir_name)
            with open(filename, "w") as f:
                f.write("--- Personal Assistant Summary ---\n")
                for key in sorted(user_data.keys()):
                    f.write(f"{key}: {user_data[key]}\n")
                f.write("----------------------------------\n")
            print(f"Your summary has been saved to '{filename}'.")
            break
        except IOError as e:
            print(f"Error saving file: {e}. Please check the path and try again.")
        except Exception as e:
            print(f"An unexpected error occurred: {e}. Please try again.")
            def rate_assistant(filename="assistant_ratings.txt"):
    while True:
        try:
            rating = int(input("\nPlease rate this assistant (1-5 stars, 5 being best): "))
            if 1 <= rating <= 5:
                timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
                with open(filename, "a") as f:
                    f.write(f"[{timestamp}] Rating: {rating} stars\n")
                print(f"Thank you for rating the assistant with {rating} stars!")
                break
            else:
                print("Invalid rating. Please enter a number between 1 and 5.")
        except ValueError:
            print("Invalid input. Please enter a number.")
        except IOError as e:
            print(f"Error saving rating: {e}")
            def main():
    while True:
        user_info = get_user_info()
        display_summary(user_info)

        save_option = input("Would you like to save this summary to a file? (yes/no): ").lower()
        if save_option == "yes":
            save_to_file(user_info)

        rate_assistant()

        restart_option = input("\nWould you like to restart the program? (yes/no): ").lower()
        if restart_option != "yes":
            print("Thank you for using the Simple Personal Assistant. Goodbye!")
            break
            if __name__ == "__main__":
            main()
