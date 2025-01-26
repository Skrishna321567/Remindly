# Remindly
homework remainder app
# Team name
SNS
# Team members
Swathi Krishna P S,
Sreeva V G
# Project description
We are trying to create a reminder app which reminds about hoeworks to students.
# The Problem statement
Many students struggle to keep track of their homework assignments, leading to missed deadlines, poor grades, and increased stress. Existing solutions like paper planners, digital calendars, or reminders from teachers often prove inadequate, as they can be easily forgotten, lost, or overlooked.
# The solution
Provide a user-friendly platform for students to track and manage homework and assignments.
 Send timely reminders and notifications to ensure students stay on top of their work.
 Facilitate communication between students, teachers, and parents.
 Help students develop essential time management and organization skills.
# Technical details
 Frontend 
 user interface: design a user friendly UI using a kivy.
 User interface components : Use widgets like text input, buttons, and labels to create UI.
 Layout management : Use layout managers like boxlayout and gridlayout to arrange UI components.
 Backend
 Programming language : Python
 # Implementation
 Install required libraries, 
 pip3 install Kivy
 # Create remindly
 The code used is 
import kivy
from kivy.app import App
from kivy.uix.boxlayout import BoxLayout
from kivy.uix.label import Label
from kivy.uix.button import Button
from kivy.uix.textinput import TextInput
from kivy.clock import Clock
from datetime import datetime

class ReminderApp(BoxLayout):
    def __init__(self, **kwargs):
        super(ReminderApp, self).__init__(**kwargs)
        self.orientation = 'vertical'

        # Title
        self.title = Label(text='Reminder App', font_size=30)
        self.add_widget(self.title)

        # Reminder input
        self.reminder_input = TextInput(hint_text='Enter reminder', font_size=20)
        self.add_widget(self.reminder_input)

        # Time input
        self.time_input = TextInput(hint_text='Enter time (HH:MM)', font_size=20)
        self.add_widget(self.time_input)

        # Add reminder button
        self.add_button = Button(text='Add Reminder', font_size=20)
        self.add_button.bind(on_press=self.add_reminder)
        self.add_widget(self.add_button)

        # Reminders list (as a list of tuples)
        self.reminders = []
        self.reminders_list = Label(text='Reminders:', font_size=20)
        self.add_widget(self.reminders_list)

        # Update reminders every minute
        Clock.schedule_interval(self.update_reminders, 60)

    def add_reminder(self, instance):
        reminder = self.reminder_input.text
        time = self.time_input.text
        if reminder and time:
            self.reminders.append((reminder, time))
            self.update_reminders_list()
            self.reminder_input.text = ''
            self.time_input.text = ''

    def update_reminders(self, dt):
        current_time = datetime.now().strftime('%H:%M')
        for reminder, reminder_time in self.reminders:
            if current_time == reminder_time:
                print(f'Reminder: {reminder}')

    def update_reminders_list(self):
        reminders_text = 'Reminders:\n'
        for reminder, time in self.reminders:
            reminders_text += f'{reminder} - {time}\n'
        self.reminders_list.text = reminders_text

class ReminderAppApp(App):
    def build(self):
        return ReminderApp()

if __name__ == '__main__':
    ReminderAppApp().run()

