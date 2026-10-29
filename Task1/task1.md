# 1. Problem Statement
Develop a Python program to calculate a patient's hospital bill by accepting consultation, diagnostic, and treatment charges. Apply conditional concessions based on the patient category and billing amount. Validate the inputs to prevent negative charges and classify patients according to the supplied payment policy. Finally, display the subtotal, concession, final bill, payment class, and patient category.
# 2. Algorithm
1. Start the program.
2. Read the patient's name and category.
3. Accept consultation, diagnostic, and treatment charges.
4. Validate all inputs and reject negative values.
5. Calculate the subtotal by adding all charges.
6. Apply the concession according to the patient category:
   - Senior citizen: 20%
   - Government employee: 15%
   - Normal patient: 0%
7. If the subtotal exceeds ₹10,000, apply an additional 5% concession.
8. Calculate the final bill by subtracting the total concession.
9. Classify the patient:
   - Below ₹2,000: Class A — Self Pay
   - ₹2,000 to ₹10,000: Class B — Insurance/Partial
   - Above ₹10,000: Class C — Corporate/Government
10. Display the bill details and patient classification.
11. Stop.
# 3. Flowchart (Mermaid)
```Mermaid
flowchart TD
    A([Start]) --> B[/Enter patient details and charges/]
    B --> C{Inputs valid?}
    C -- No --> D[Display error message]
    D --> B
    C -- Yes --> E[Calculate subtotal]
    E --> F[Apply category concession]
    F --> G{Subtotal > 10000?}
    G -- Yes --> H[Apply extra 5% concession]
    G -- No --> I[Calculate final bill]
    H --> I
    I --> J[Classify patient]
    J --> K[/Display bill and classification/]
    K --> L([End])
```
# 4. Source Code (Python)

def get_charge(prompt):
    while True:
        try:
            charge = float(input(prompt))
            if charge < 0:
                print("Error: Charge cannot be negative.")
            else:
                return charge
        except ValueError:
            print("Error: Enter a valid number.")


def classify_patient(amount):
    if amount < 2000:
        return "Class A - Self Pay"
    elif amount <= 10000:
        return "Class B - Insurance/Partial"
    else:
        return "Class C - Corporate/Government"


def main():
    print("=== Hospital Billing System ===")

    name = input("Enter patient name: ").strip()
    if not name:
        print("Error: Patient name cannot be empty.")
        return

    category = input(
        "Enter category (Senior/Government/Normal): "
    ).strip().lower()

    if category not in ("senior", "government", "normal"):
        print("Error: Invalid patient category.")
        return

    consultation = get_charge("Consultation charge: ")
    diagnostic = get_charge("Diagnostic charge: ")
    treatment = get_charge("Treatment charge: ")

    subtotal = consultation + diagnostic + treatment

    # Category-based concession
    if category == "senior":
        rate = 0.20
    elif category == "government":
        rate = 0.15
    else:
        rate = 0.0

    concession = subtotal * rate

    # Additional 5% concession if subtotal exceeds 10000
    if subtotal > 10000:
        concession += subtotal * 0.05

    final_bill = subtotal - concession
    patient_class = classify_patient(final_bill)

    print("\n===== BILL DETAILS =====")
    print(f"Patient Name       : {name}")
    print(f"Patient Category   : {category.title()}")
    print(f"Consultation       : Rs. {consultation:.2f}")
    print(f"Diagnostic         : Rs. {diagnostic:.2f}")
    print(f"Treatment          : Rs. {treatment:.2f}")
    print(f"Subtotal           : Rs. {subtotal:.2f}")
    print(f"Total Concession   : Rs. {concession:.2f}")
    print(f"Final Bill         : Rs. {final_bill:.2f}")
    print(f"Payment Class      : {patient_class}")


if __name__ == "__main__":
    main()
# 5. Sample Input 
Enter patient name: Ramesh
Enter category (Senior/Gove
rnment/Normal): Senior
Consultation charge: 800
Diagnostic charge: 1200
Treatment charge: 3000
# 6. Sample Output
===== BILL DETAILS =====
Patient Name       : Ramesh
Patient Category   : Senior
Consultation       : Rs. 800.00
Diagnostic         : Rs. 1200.00
Treatment          : Rs. 3000.00
Subtotal           : Rs. 5000.00
Total Concession   : Rs. 1000.00
Final Bill         : Rs. 4000.00
Payment Class      : Class B - Insurance/Partial
# 7. Screenshot
<img width="1195" height="859" alt="image" src="https://github.com/user-attachments/assets/ec1a8a9b-d04e-48d0-8b4f-31a1a9645d36" />
 
