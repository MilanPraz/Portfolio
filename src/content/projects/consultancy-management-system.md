---
title: Task Management Kanban Board
description: A task management system that allows users to create, assign, and track tasks using a Kanban-style board.
pubDate: 2023-08-01
liveURL: https://kanban.milanprajapati.com.np
githubURL: https://github.com/MilanPraz/kanban-board
# heroImage: ../assets/consultancy-management-system.png
stacks: ['React', 'TypeScript', 'Node.js', 'Drag and Drop']
---

## Overview

The Consultancy Student Management System is a modern, Kanban-style dashboard designed to help consultancy teams efficiently manage students, tasks, and progress across multiple stages.

The application focuses on clarity, responsiveness, and usability, enabling users to visualize workflows, track status changes, and manage responsibilities through an intuitive drag-and-drop interface.

## Key Challenges

- Designing a grid-based Kanban layout that remains responsive across screen sizes while maintaining clear task separation.
- Implementing smooth and intuitive drag-and-drop interactions without compromising performance.
- Preventing unnecessary re-renders while frequently updating board state.
- Maintaining a clean UI that supports complex workflows without overwhelming users.

## Key Learnings

- Leveraging Next.js with TypeScript significantly improved maintainability and confidence while refactoring complex UI logic.
- React Beautiful DnD provided a powerful abstraction for handling drag-and-drop behavior while still requiring careful state management.
- Tailwind CSS enabled rapid UI iteration and consistent spacing across the board layout.
- Breaking the board into reusable components simplified future feature additions and improvements.

## Uniqueness

- A minimal, distraction-free Kanban experience tailored for consultancy-style student tracking.
- Real-time visual feedback during drag-and-drop interactions for better usability.
- Clean separation of concerns between board, column, and card components.
- Designed with extensibility in mind to support future workflow enhancements.

## Impact

- Improved task visibility and workflow clarity for consultancy teams.
- Reduced manual tracking by centralizing student progress in a single interface.
- Enabled faster task updates and better coordination through intuitive interactions.
- Provided a scalable frontend foundation suitable for expanding into a full management system.
