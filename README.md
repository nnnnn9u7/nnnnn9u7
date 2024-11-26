import streamlit as st

# شاشة تسجيل الدخول
def login_screen():
    st.title("Login Screen")
    username = st.text_input("Username")
    password = st.text_input("Password", type='password')
    
    if st.button("Login"):
        st.session_state['user'] = username
        st.session_state['logged_in'] = True
        st.success(f"Welcome {username}!")

# شاشة اختيار الجدول الزمني
def select_schedule():
    st.title("Select Schedule")
    schedules = ["8:00 AM - Bus A", "10:00 AM - Bus B", "12:00 PM - Bus C"]
    selected_schedule = st.selectbox("Select Schedule", schedules)
    
    if st.button("Next"):
        st.session_state['selected_schedule'] = selected_schedule
        st.success(f"Selected Schedule: {selected_schedule}")
        show_booking()

# شاشة الحجز
def show_booking():
    st.title("Book Seat")
    seats = ["1A", "1B", "2A", "2B", "3A", "3B"]
    selected_seat = st.selectbox("Select Seat", seats)
    
    if st.button("Next"):
        st.session_state['selected_seat'] = selected_seat
        st.success(f"Seat {selected_seat} booked!")

# شاشة التتبع
def track_bus():
    st.title("Track Bus")
    st.write("Your Bus is 3 minutes away!")
    if st.button("Confirm"):
        st.success("Ride Confirmed! Enjoy your trip.")

# شاشة التأكيد
def confirmation_screen():
    st.title("Confirmation")
    st.write("Your seat has been successfully booked!")
    st.write("Enjoy your trip!")

# قائمة اختيار الواجهة
if 'logged_in' not in st.session_state:
    st.session_state['logged_in'] = False

if not st.session_state['logged_in']:
    login_screen()
else:
    if 'selected_schedule' not in st.session_state:
        select_schedule()
    elif 'selected_seat' not in st.session_state:
        show_booking()
    else:
        track_bus()
