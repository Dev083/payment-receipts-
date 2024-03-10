# Payment Receipts Generator

Creating payment receipts is an essential feature for any business, whether it's an e-commerce website or a local store. This Python project demonstrates how to generate transaction receipts using ReportLab to create PDFs. ReportLab is a powerful library for PDF generation in Python, providing various customization options.

## Installation

To install the necessary dependencies, run:

```bash
pip install reportlab
```

## Approach

- **Importing Modules**: The project utilizes modules from ReportLab for PDF generation.
- **Data Structure**: Receipt data is organized as a list of lists, where the first index of the outer list represents the headers.
- **Document Template**: A simple document template is created with the A4 paper size.
- **Styling**: Sample style sheets are used to format the text and tables within the receipt.
- **Building PDF**: The receipt is constructed by combining the data and styles into a PDF document.

## Implementation

```python
from reportlab.platypus import SimpleDocTemplate, Table, Paragraph, TableStyle
from reportlab.lib import colors
from reportlab.lib.pagesizes import A4
from reportlab.lib.styles import getSampleStyleSheet

# Data for the receipt
DATA = [
    ["Date", "Name", "Subscription", "Price (Rs.)"],
    ["16/11/2020", "Full Stack Development with React & Node JS - Live", "Lifetime", "10,999.00/-"],
    ["16/11/2020", "Geeks Classes: Live Session", "6 months", "9,999.00/-"],
    ["Sub Total", "", "", "20,9998.00/-"],
    ["Discount", "", "", "-3,000.00/-"],
    ["Total", "", "", "17,998.00/-"],
]

# Creating a base document template of page size A4
pdf = SimpleDocTemplate("receipt.pdf", pagesize=A4)

# Standard stylesheet defined within ReportLab itself
styles = getSampleStyleSheet()

# Fetching the style of top-level heading (Heading1)
title_style = styles["Heading1"]
title_style.alignment = 1

# Creating the paragraph with the heading text and passing the styles
title = Paragraph("GeeksforGeeks", title_style)

# Defining the style for the table
style = TableStyle([
    ("BOX", (0, 0), (-1, -1), 1, colors.black),
    ("GRID", (0, 0), (4, 4), 1, colors.black),
    ("BACKGROUND", (0, 0), (-1, 0), colors.gray),
    ("TEXTCOLOR", (0, 0), (-1, 0), colors.whitesmoke),
    ("ALIGN", (0, 0), (-1, -1), "CENTER"),
    ("BACKGROUND", (0, 1), (-1, -1), colors.beige),
])

# Creating a table object and passing the style to it
table = Table(DATA, style=style)

# Building the PDF document
pdf.build([title, table])
```

This project provides a simple yet effective way to generate payment receipts in PDF format using Python.
