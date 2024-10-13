# Scheduler Library for React

Welcome to the **Scheduler Library**! This React-based scheduling library helps you manage events across daily, weekly, and monthly views with customizable modals and smooth animations.

## Table of Contents
- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
  - [Scheduler Wrapper](#scheduler-wrapper)
- [Context Provider Setup](#context-provider-setup)
  - [Handlers Explained](#handlers-explained)
  - [Getters Explained](#getters-explained)
- [Custom Modals and Styling](#custom-modals-and-styling)
- [Contributing](#contributing)
- [License](#license)

---

## Features
- **Daily, Weekly, and Monthly Views**: Navigate through events by day, week, or month.
- **Add, Update, Remove Events**: Manage events easily with modals and state management.
- **Smooth Animations**: Utilize `framer-motion` for smooth transitions.
- **Custom Event Styling**: Adjust layout dynamically based on event overlap and size.
- **Context Management**: Use the Scheduler context with React's `useReducer`.
- **Integration with Modals**: Support for `@nextui-org` components and custom modals.

---

## Installation

To get started, clone the repository from GitHub:

```bash
git clone https://github.com/your-username/scheduler-library.git
cd scheduler-library
npm install
```

---

## Usage

### Scheduler Wrapper

To use the scheduler in your project, call the `SchedulerView` inside a wrapper component:

```javascript
import React from "react";
import SchedulerView from "../view/schedular-view";

export default function SchedulerWrapper() {
  return (
    <div className="w-full">
      <h1 className="tracking-tighter font-semibold text-8xl mb-10">
        Event Schedule
      </h1>
      <SchedulerView />
    </div>
  );
}
```

This wrapper ensures the **SchedulerView** is correctly rendered inside your component tree.

---

## Context Provider Setup

Wrap your application with the `SchedulerProvider` to manage event state and actions.

### Example:

```javascript
import { SchedulerProvider } from './context/SchedulerContext';
import SchedulerWrapper from './components/SchedulerWrapper';

function App() {
  return (
    <SchedulerProvider>
      <SchedulerWrapper />
    </SchedulerProvider>
  );
}
```

---

## Handlers Explained

Handlers define logic for managing event styling. This ensures that overlapping events display correctly and that events are positioned dynamically within the scheduler view.

```javascript
handlers.handleEventStyling(event, dayEvents);
```

### Breakdown:
- **`handleEventStyling(event, dayEvents)`**: 
  - Calculates the top position and height for each event.
  - Adjusts the event's position if it overlaps with others.
  - Returns an object with:
    - `height`: Calculated event height.
    - `top`: Top offset for event positioning.
    - `left`: Horizontal positioning if there are multiple events in the same slot.
    - `zIndex`: Stacking order for overlapping events.
    - `maxWidth`, `minWidth`: Width management for overlapping events.

---

## Getters Explained

Getters provide utility methods for retrieving and manipulating scheduling data.

### List of Getters:

1. **`getDaysInMonth(month, year)`**:  
   - Returns an array of days in a specific month, each with its corresponding events.
   ```javascript
   const days = getters.getDaysInMonth(9, 2024);
   ```

2. **`getEventsForDay(day, currentDate)`**:  
   - Filters and returns the list of events for a specific day.
   ```javascript
   const events = getters.getEventsForDay(12, new Date());
   ```

3. **`getDaysInWeek(week, year)`**:  
   - Returns an array of `Date` objects for the days in a given week of the year.
   ```javascript
   const weekDays = getters.getDaysInWeek(42, 2024);
   ```

4. **`getWeekNumber(date)`**:  
   - Calculates the week number of a given date in the year.
   ```javascript
   const weekNumber = getters.getWeekNumber(new Date());
   ```

5. **`getDayName(day)`**:  
   - Returns the name of the day (e.g., "Mon", "Tue").
   ```javascript
   const dayName = getters.getDayName(1); // Output: "Mon"
   ```

---

## Custom Modals and Styling

The library integrates with `@nextui-org` for modals and supports event management through user interactions.

### Example Modal Usage:

```javascript
showModal({
  title: "Add Event",
  body: <AddEventModal />,
  getter: async () => ({
    startDate: new Date(),
    endDate: new Date(Date.now() + 60 * 60 * 1000), // 1 hour later
  }),
});
```

---

## Contributing

We welcome contributions! If you'd like to contribute:
1. Fork the repository.
2. Create a new branch for your feature.
3. Submit a pull request for review.

---

## License

This project is licensed under the MIT License.

---

Thank you for using the my Scheduler Library! Feel free to reach out if you encounter any issues or need further assistance.