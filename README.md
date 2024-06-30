
```python
import json
import os
from datetime import datetime

class CareerDashboard:
    def __init__(self):
        self.data_file = "career_data.json"
        self.career_data = self.load_data()

    def load_data(self):
        if os.path.exists(self.data_file):
            with open(self.data_file, 'r') as f:
                return json.load(f)
        return {
            "skills": [],
            "projects": [],
            "education": [],
            "work_experience": [],
            "goals": []
        }

    def save_data(self):
        with open(self.data_file, 'w') as f:
            json.dump(self.career_data, f, indent=2)

    def add_skill(self, skill):
        self.career_data["skills"].append({"name": skill, "date_added": str(datetime.now().date())})
        self.save_data()

    def add_project(self, name, description):
        self.career_data["projects"].append({
            "name": name,
            "description": description,
            "date_added": str(datetime.now().date())
        })
        self.save_data()

    def add_education(self, institution, degree, year):
        self.career_data["education"].append({
            "institution": institution,
            "degree": degree,
            "year": year
        })
        self.save_data()

    def add_work_experience(self, company, position, start_date, end_date=None):
        self.career_data["work_experience"].append({
            "company": company,
            "position": position,
            "start_date": start_date,
            "end_date": end_date if end_date else "Present"
        })
        self.save_data()

    def add_goal(self, goal, target_date):
        self.career_data["goals"].append({
            "goal": goal,
            "target_date": target_date,
            "date_added": str(datetime.now().date())
        })
        self.save_data()

    def display_dashboard(self):
        print("\n===== Career Dashboard =====")
        print("\nSkills:")
        for skill in self.career_data["skills"]:
            print(f"- {skill['name']} (Added: {skill['date_added']})")

        print("\nProjects:")
        for project in self.career_data["projects"]:
            print(f"- {project['name']}: {project['description']} (Added: {project['date_added']})")

        print("\nEducation:")
        for edu in self.career_data["education"]:
            print(f"- {edu['degree']} from {edu['institution']} ({edu['year']})")

        print("\nWork Experience:")
        for exp in self.career_data["work_experience"]:
            print(f"- {exp['position']} at {exp['company']} ({exp['start_date']} - {exp['end_date']})")

        print("\nGoals:")
        for goal in self.career_data["goals"]:
            print(f"- {goal['goal']} (Target: {goal['target_date']}, Added: {goal['date_added']})")

def main():
    dashboard = CareerDashboard()

    while True:
        print("\n1. Add Skill")
        print("2. Add Project")
        print("3. Add Education")
        print("4. Add Work Experience")
        print("5. Add Goal")
        print("6. Display Dashboard")
        print("7. Exit")

        choice = input("Enter your choice (1-7): ")

        if choice == '1':
            skill = input("Enter skill name: ")
            dashboard.add_skill(skill)
        elif choice == '2':
            name = input("Enter project name: ")
            description = input("Enter project description: ")
            dashboard.add_project(name, description)
        elif choice == '3':
            institution = input("Enter institution name: ")
            degree = input("Enter degree name: ")
            year = input("Enter graduation year: ")
            dashboard.add_education(institution, degree, year)
        elif choice == '4':
            company = input("Enter company name: ")
            position = input("Enter position: ")
            start_date = input("Enter start date (YYYY-MM-DD): ")
            end_date = input("Enter end date (YYYY-MM-DD) or leave blank if current: ")
            dashboard.add_work_experience(company, position, start_date, end_date if end_date else None)
        elif choice == '5':
            goal = input("Enter your goal: ")
            target_date = input("Enter target date (YYYY-MM-DD): ")
            dashboard.add_goal(goal, target_date)
        elif choice == '6':
            dashboard.display_dashboard()
        elif choice == '7':
            print("Thank you for using the Career Dashboard. Goodbye!")
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()
```

This Python script creates a simple career dashboard that allows you to track various aspects of your professional development. Here's a breakdown of its main features:

1. Skills tracking
2. Project logging
3. Education history
4. Work experience records
5. Goal setting

The dashboard uses a JSON file (`career_data.json`) to store your data persistently. This means your information will be saved between sessions.

To use this dashboard:

1. Copy the code into a Python file (e.g., `career_dashboard.py`).
2. Run the script using Python: `python career_dashboard.py`
3. Follow the on-screen prompts to add information or view your dashboard.

This dashboard provides a foundation that you can easily expand upon. For example, you might want to add features like:

- Editing or deleting existing entries
- Sorting and filtering capabilities
- Data visualization (e.g., skills growth over time)
- Exporting data to different formats (CSV, PDF)
