import streamlit as st
from datetime import datetime, timedelta

st.title("Cycle Tracker")

last_cycle = st.date_input("Last cycle date")
cycle_length = st.number_input("Cycle length (days)", min_value=20, max_value=40, value=28)

if st.button("Calculate next cycle"):
    next_cycle = last_cycle + timedelta(days=cycle_length)
    ovulation = next_cycle - timedelta(days=14)
    fertile_window_start = ovulation - timedelta(days=3)
    fertile_end = ovulation + timedelta(days=1)

    st.success(f"Next cycle: {next_cycle.strftime('%Y-%m-%d')}")
    st.info(f"Ovulation day: {ovulation.strftime('%Y-%m-%d')}")
    st.warning(f"Fertile window: {fertile_window_start.strftime('%Y-%m-%d')} to {fertile_end.strftime('%Y-%m-%d')}")

# Ask the user about their PCOS condition
st.subheader("🩺 Health Question")
pcos_status = st.radio(
    "Have you been diagnosed with PCOS (Polycystic Ovary Syndrome)?",
    options=["No", "Yes"],
    index=0
)

if pcos_status == "Yes":
    st.header("About PCOS (Polycystic Ovary Syndrome)")
    st.markdown("""
    **PCOS (Polycystic Ovary Syndrome)** is a hormonal disorder that can cause irregular periods, excess androgen levels, and polycystic ovaries.

    **Common symptoms:**
    - Irregular or missed periods
    - Excess hair growth (hirsutism)
    - Acne or oily skin
    - Weight gain or difficulty losing weight

    **Possible treatments and medications:**
    - **Lifestyle changes:** Healthy diet, regular exercise, and weight management can help regulate cycles.
    - **Medications:**
        - *Birth control pills* to regulate periods and reduce androgen levels.
        - *Metformin* to improve insulin resistance and help with weight loss.
        - *Clomiphene* or *Letrozole* to stimulate ovulation if trying to conceive.
        - *Anti-androgens* (like spironolactone) to reduce excess hair and acne.
    - **Other therapies:** Hair removal treatments, acne treatments, and counseling for emotional support.

    **Always consult a healthcare provider for diagnosis and personalized treatment.**

    [More information on PCOS](https://www.womenshealth.gov/a-z-topics/polycystic-ovary-syndrome)
    """)
    

    
