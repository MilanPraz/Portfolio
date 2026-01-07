---
title: Database Schema Visualizer
description: A database schema visualizer that allows users to visualize their database schema.
pubDate: 'May 14 2023'
# heroImage: ../assets/database-schema-visualizer.png
liveURL: https://database-schema-visualizer.vercel.app/
githubURL: https://github.com/MilanPraz/db-visualizer
stacks: ['React', 'TypeScript', 'D3.js']
---

## Overview

The Database Schema Visual Editor is a web-based tool designed to simplify database design through an interactive, visual interface. It allows users to create, edit, and visualize database schemas using draggable nodes and relational edges.

The tool focuses on improving clarity and productivity by bridging the gap between text-based schema definitions and visual database modeling.

## Key Challenges

- Designing an intuitive canvas-based interface that supports complex database relationships.
- Managing real-time updates while dragging nodes and creating relational edges.
- Parsing text-based DBML schemas into structured visual representations.
- Ensuring smooth interactions and performance when working with large schemas.

## Key Learnings

- Using React with @xyflow/react enabled flexible and highly interactive diagram-based UI development.
- Implementing DBML parsing required careful handling of schema definitions and relationships.
- Structuring application state effectively simplified node positioning, edge updates, and diagram consistency.
- Modularizing diagram components improved maintainability and future extensibility.

## Uniqueness

- Real-time visual schema editing with draggable nodes and relational edges.
- Automatic generation of tables and relationships from DBML input.
- Clean, developer-focused UI optimized for database design workflows.
- Combines text-based schema definition with visual feedback for better understanding.

## Impact

- Reduced friction in database design by providing instant visual feedback.
- Helped developers quickly validate and iterate on schema structures.
- Enabled faster onboarding for team members unfamiliar with complex database relationships.
- Served as a practical tool for planning, documenting, and communicating database designs.
