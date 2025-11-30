# TaskRankerModel

This project provides a simple machine learning model for ranking tasks by priority based on their deadline, difficulty, and weight. It is implemented in a Jupyter Notebook and uses a CSV file for input data.

## Files

- **TaskRankerModel.ipynb**: Main notebook containing the code for the task ranking model, data loading, and scoring logic.
- **tasks.csv**: Example dataset of tasks with columns: `name`, `difficulty`, `weight`, and `deadline`.

## How It Works

1. **Data Loading**: Reads tasks from `tasks.csv` using pandas.
2. **Model**: The `TaskPriorityModel` class calculates a priority score for each task based on:
   - Days until deadline
   - Difficulty
   - Weight
3. **Scoring**:
   - Urgency is higher for tasks closer to their deadline.
   - Difficulty and weight are added to the score.
   - Optionally, scores can be normalized to percentages.
4. **Sorting**: Tasks are sorted by their priority score in descending order.
5. **Adding Tasks**: New tasks can be added and scored dynamically.

## Example Usage

- Load and display tasks:
  ```python
  df = pd.read_csv('tasks.csv')
  df['deadline'] = pd.to_datetime(df['deadline'])
  model = TaskPriorityModel()
  df['priority_score'] = model.predict_batch_df(df)
  df = df.sort_values('priority_score', ascending=False).reset_index(drop=True)
  df
  ```
- Add a new task:
  ```python
  new_task = {
      'name': 'Quiz',
      'difficulty': 2,
      'weight': 5,
      'deadline': '2025-12-01'
  }
  df = pd.concat([df, pd.DataFrame([new_task])], ignore_index=True)
  df['priority_score'] = model.predict_batch_df(df)
  df = df.sort_values('priority_score', ascending=False).reset_index(drop=True)
  df
  ```

## Requirements
- Python
- pandas

## Purpose
This notebook helps you prioritize tasks efficiently, making it useful for students, project managers, or anyone needing to rank tasks by urgency and importance.
