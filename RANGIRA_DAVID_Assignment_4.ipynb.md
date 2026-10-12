# Part A: Router, handlers, fines, and greeting

def handle_greeting(message, memory=None):
    return "Hello! Welcome to the campus library chatbot. How can I help you today?"


def handle_hours(message, memory=None):
    return "The library opening hours are listed in the library information."


def handle_borrow(message, memory=None):
    return "You can borrow books using your student library account. Please check the borrowing rules for loan periods."


def handle_renew(message, memory=None):
    return "You can renew eligible borrowed books through your library account."


def handle_fines(message, memory=None):
    import re

    match = re.search(r"(\d+)\s*days?", message.lower())

    if not match:
        return "How many days overdue is the book?"

    days_overdue = int(match.group(1))
    daily_rate = 500
    fine = days_overdue * daily_rate

    return f"Your fine for {days_overdue} overdue day(s) is {fine} RWF."


def handle_rooms(message, memory=None):
    return "I can help you book a study room. What date and time would you like?"


def handle_printing(message, memory=None):
    return "You can use the campus library printing service. Please check the available printing options."


# Connect each intent to its handler
HANDLERS = {
    "greeting": handle_greeting,
    "hours": handle_hours,
    "borrow": handle_borrow,
    "renew": handle_renew,
    "fines": handle_fines,
    "rooms": handle_rooms,
    "printing": handle_printing,
}


# Router function
def route_message(intent, message, memory=None):
    handler = HANDLERS.get(intent)

    if handler is None:
        return "Sorry, I don't understand that request yet."

    return handler(message, memory)
