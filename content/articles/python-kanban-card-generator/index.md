+++
author = "Tom Claessens"
title = "Python kanban card generator"
date = "2025-01-28"
description = "Streamline your pantry management with the Kanban Card Generator, a Python-based tool for creating customizable QR-enabled Kanban cards."
tags = ["technology"]
showtoc = false
TocSide = "right"
+++
Managing pantry inventory can be a daunting task, often leading to overstocking or running out of essential items. To address this challenge, I developed the [Kanban Card Generator](https://github.com/claesto/kanban-card-generator), a Python-powered tool designed to streamline pantry management by generating QR-enhanced Kanban cards.

## Project overview
Inspired by the Kanban system—a scheduling method widely used in just-in-time (JIT) manufacturing—I adapted its principles for personal pantry management. The core idea is to create visual cues that signal when it's time to replenish specific items, thereby maintaining optimal stock levels.

The Kanban Card Generator produces business card-sized labels containing essential product information:

- **Product Type**: The category or name of the item
- **Manufacturer**: The brand or producer of the item
- **Store of Purchase**: Where the item is typically bought
- **Kanban Levels**: Indicators that help determine when to reorder
- **Reorder Quantity**: The amount to purchase when restocking

A prominent feature of each card is a QR code, generated using the [Segno library](https://pypi.org/project/segno/). This QR code integrates seamlessly with a custom macOS and iOS Shortcut, allowing for quick addition of items to a designated list, such as a grocery list.

## Key features
- **Python-Powered**: Utilizes Python for efficient data processing and card generation.
- **QR Code Integration**: Generates QR codes for swift item logging via mobile devices.
- **Customizable Templates**: Allows for personalization of card design to suit individual preferences.
- **Cross-Platform Compatibility**: Works seamlessly with macOS and iOS Shortcuts for enhanced usability.

## Getting started
To setup the Kanban Card Generator:

0. Prerequisite: you have the macOS/iOS Shortcut "[AddToList](https://www.icloud.com/shortcuts/609528f7b75b441bb34834c92f07b175)" installed.

1. **Clone the Repository**:
   ```bash
   $ git clone https://github.com/claesto/kanban-card-generator.git
   $ cd kanban-card-generator
   ```
2. Activate the Python virtual environment:
   ```bash
   $ python -m venv venv
   $ venv/bin/python venv/bin/activate
   ```
2. **Install Dependencies**: Ensure you have Python installed, then install the required libraries:
   ```bash
   $ venv/bin/python -m pip install -r requirements.txt
   ```
3. **Configure Your Data**: Customize the kanbancard.py script with your inventory details, including product names, manufacturers, stores, Kanban levels, and reorder quantities.
4. **Generate Kanban Cards**: Run the script to generate your personalized Kanban cards:
   ```bash
   venv/bin/python kanbancard.py
   ```
5. **Print and Use**: Print the generated cards and attach them to your pantry items. Use the QR codes with the macOS and iOS Shortcut to manage your inventory efficiently.

If all went as expected, if you scan the QR code for a specific item, this item should be added to your [Reminders](https://www.icloud.com/reminders/) list of choice.

## Future enhancements
Right now I'm not really looking for specific enhancements. I don't have to manage a large inventory, this is after all to make managing our pantry/storage a bit easier. However feel free to iterate on the code, it's available under the **Unlicense** license.

Some ideas:
- **Database integration**: Implementing a database to manage larger inventories
- **Enhanced customization/templates**: Offering more design options for the generated kanban cards
- **Mobile application**: specifically tailored to inventory/stock management

Contributions and feedback are welcome! Feel free to fork the repository, submit [pull requests](https://github.com/claesto/kanban-card-generator/pulls), or [open issues](https://github.com/claesto/kanban-card-generator/issues) on GitHub.

By leveraging this tool, you can transform your pantry management into a streamlined, efficient process, ensuring you always have the essentials on hand without overstocking.