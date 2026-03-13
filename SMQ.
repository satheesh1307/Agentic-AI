import streamlit as st
import random
import datetime

st.set_page_config(page_title="Smart Healthcare System", layout="wide")

st.title("Agentic AI Smart Healthcare Queue System")

# -------------------------
# User Login
# -------------------------

if "user" not in st.session_state:
    st.session_state.user = ""

name = st.text_input("Enter Your Name")

if name:
    st.session_state.user = name
    st.success(f"Welcome {name}")

# -------------------------
# Hospital Data
# -------------------------

if "hospitals" not in st.session_state:

    st.session_state.hospitals = {

        "City Hospital": {
            "General Physician": {"waiting":5,"status":"Available"},
            "Cardiologist": {"waiting":3,"status":"Available"},
            "Dermatologist": {"waiting":4,"status":"On Leave"}
        },

        "Apollo Clinic": {
            "General Physician": {"waiting":6,"status":"Available"},
            "ENT Specialist": {"waiting":2,"status":"Available"},
            "Orthopedic": {"waiting":5,"status":"Busy"}
        },

        "Care Medical Center": {
            "Pediatrician": {"waiting":4,"status":"Available"},
            "Neurologist": {"waiting":2,"status":"Available"},
            "General Physician": {"waiting":3,"status":"Available"}
        }
    }

hospitals = st.session_state.hospitals

# -------------------------
# Menu
# -------------------------

menu = st.sidebar.selectbox(
    "Menu",
    [
        "Hospital Search",
        "Join Queue",
        "Queue Status",
        "Appointment Booking",
        "Symptom Checker",
        "AI Assistant",
        "Medicine Reminder",
        "Emergency SOS",
        "Hospital Dashboard"
        "Admin Dashboard"
    ]
)

# -------------------------
# Hospital Search
# -------------------------

if menu == "Hospital Search":

    st.header("Nearby Hospitals")

    for hospital in hospitals:

        st.subheader(hospital)

        for doctor,data in hospitals[hospital].items():

            st.write(f"{doctor} | Waiting: {data['waiting']} | Status: {data['status']}")

# -------------------------
# Join Queue
# -------------------------

elif menu == "Join Queue":

    st.header("Join Hospital Queue")

    hospital = st.selectbox("Select Hospital", list(hospitals.keys()))

    available_doctors = [
        doc for doc,data in hospitals[hospital].items()
        if data["status"] == "Available"
    ]

    if available_doctors:

        doctor = st.selectbox("Select Doctor", available_doctors)

        if st.button("Join Queue"):

            token = random.randint(100,999)
            waiting = hospitals[hospital][doctor]["waiting"]

            wait_time = waiting * 5

            st.session_state.token = token
            st.session_state.doctor = doctor
            st.session_state.waiting = waiting

            st.success(f"Token Number: {token}")
            st.info(f"Approx Waiting Time: {wait_time} minutes")

        if "token" in st.session_state:

            if st.button("Check-In"):

                st.success("You are added to final queue")

    else:

        st.warning("No doctors currently available")

# -------------------------
# Queue Status
# -------------------------

elif menu == "Queue Status":

    st.header("Queue Status")

    if "token" in st.session_state:

        st.write(f"Your Token: {st.session_state.token}")
        st.write(f"Doctor: {st.session_state.doctor}")

        remaining = st.session_state.waiting

        st.write(f"Patients before you: {remaining}")

    else:

        st.warning("You have not joined the queue")

# -------------------------
# Appointment Booking
# -------------------------

elif menu == "Appointment Booking":

    st.header("Book Doctor Appointment")

    hospital = st.selectbox("Hospital", list(hospitals.keys()))
    doctor = st.selectbox("Doctor", list(hospitals[hospital].keys()))

    date = st.date_input("Select Date")
    time = st.time_input("Select Time")

    if st.button("Book Appointment"):

        st.success(f"Appointment booked with {doctor} on {date} at {time}")

# -------------------------
# Symptom Checker
# -------------------------

elif menu == "Symptom Checker":

    st.header("AI Symptom Checker")

    symptoms = st.multiselect(
        "Select Symptoms",
        ["Fever","Cold","Headache","Chest Pain","Skin Allergy","Stomach Pain"]
    )

    if st.button("Analyze Symptoms"):

        if "Chest Pain" in symptoms:
            doctor = "Cardiologist"

        elif "Skin Allergy" in symptoms:
            doctor = "Dermatologist"

        elif "Cold" in symptoms:
            doctor = "ENT Specialist"

        else:
            doctor = "General Physician"

        st.success(f"Suggested Doctor: {doctor}")
        st.warning("Opinion Only - Please consult a doctor")

# -------------------------
# AI Assistant
# -------------------------

elif menu == "AI Assistant":

    st.header("AI Healthcare Assistant")

    question = st.text_input("Ask your health question")

    if question:

        q = question.lower()

        if "fever" in q:
            st.write("You may consult a General Physician")

        elif "cold" in q:
            st.write("ENT Specialist consultation may help")

        elif "hospital" in q:
            st.write("Nearby hospitals are City Hospital, Apollo Clinic and Care Medical Center")

        else:
            st.write("Please consult a doctor for proper medical advice")

        st.warning("AI response is opinion only")

# -------------------------
# Medicine Reminder
# -------------------------

elif menu == "Medicine Reminder":

    st.header("Medicine Reminder")

    medicine = st.text_input("Medicine Name")
    time = st.time_input("Reminder Time")

    if st.button("Set Reminder"):

        st.success(f"Reminder set for {medicine} at {time}")

# -------------------------
# Emergency SOS
# -------------------------

elif menu == "Emergency SOS":

    st.header("Emergency Assistance")

    if st.button("Send Emergency Alert"):

        st.error("Emergency alert sent to nearby hospitals")

        st.write("Ambulance Service: 108")

# -------------------------
# Hospital Dashboard
# -------------------------

elif menu == "Hospital Dashboard":

    st.header("Hospital Staff Dashboard")

    hospital = st.selectbox("Hospital", list(hospitals.keys()))
    doctor = st.selectbox("Doctor", list(hospitals[hospital].keys()))
elif menu == "Hospital Dashboard":

    st.header("Hospital Staff Dashboard")

    hospital_list = list(hospitals.keys())

    hospital = st.selectbox("Select Hospital", hospital_list)

    st.write("Doctor List")

    for doctor in hospitals[hospital]:

        waiting = hospitals[hospital][doctor]["waiting"]
        status = hospitals[hospital][doctor]["status"]

        st.write(f"Doctor: {doctor}")
        st.write(f"Waiting Patients: {waiting}")
        st.write(f"Status: {status}")
        st.write("----------------------")

    st.subheader("Update Doctor Status")

    doctor = st.selectbox("Doctor", list(hospitals[hospital].keys()))

    new_status = st.selectbox(
        "Change Status",
        ["Available","Busy","On Leave"]
    )

    if st.button("Update Status"):

        hospitals[hospital][doctor]["status"] = new_status

        st.success("Doctor status updated")
