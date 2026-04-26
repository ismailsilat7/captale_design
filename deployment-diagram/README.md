# Deployment Diagram - CapTale

![Deployment Diagram - CapTale](Deployment%20Diagram.png)

This UML Deployment Diagram illustrates the physical architecture and runtime environment for the CapTale application on a user's machine. The primary hardware node is the User machine (desktop/laptop), which interfaces with external input peripherals (Keyboard and Mouse) and output devices (Speaker and Monitor). Inside the machine's Operating System (OS) execution environment, the main executable `CapTale.exe` utilizes the `raylib.dll` library to manage core logic. Data persistence is handled via a Local File System storage node, where the application reads static Game assets (Textures, Audio, and Fonts) and performs read/write operations on the `characterData.txt` file for saving and loading player progress. This layout highlights the clear separation between external hardware interaction, internal execution logic, and the localized file management system.

This project uses Lucidchart for deployment diagram design. You can view the diagram using the link below directly on Lucidchart:

[View the deployment diagram on Lucidchart](https://lucid.app/lucidchart/34fc0676-304f-4a26-a5fe-9313faa2f9aa/edit?view_items=fkPRQdke86cR&page=0_0&invitationId=inv_6400e92d-faf3-445f-b65f-b70644875d9e)

Alternatively, you can view or download the diagram as a PDF or PNG:

- [Download PDF](Deployment%20Diagram.pdf)
- [Download PNG](Deployment%20Diagram.png)

