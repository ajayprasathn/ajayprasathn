#include <iostream>
#include <vector>
#include <string>
#include <map>
using namespace std;  // Added semicolon

struct Course {
    string name;
    float credits;
    string grade;
    float grade_points;
};

int main() {
    int num_courses;
    float total_credits = 0, total_grade_points = 0;

    cout << "Enter number of courses: ";
    cin >> num_courses;

    vector<Course> courses;
    map<string, float> grade_points_map = {
        {"A", 4.0},
        {"B", 3.0},
        {"C", 2.0},
        {"D", 1.0},
        {"F", 0.0}
    };

    for (int i = 0; i < num_courses; i++) {
        Course course;
        cout << "\nCourse " << i + 1 << ":\n";

        cout << "Enter course name: ";
        cin >> course.name;

        while (true) {
            cout << "Enter course credits: ";
            cin >> course.credits;
            if (course.credits > 0) break;
            cout << "Credits must be a positive number.\n";
        }

        while (true) {
            cout << "Enter grade (A/B/C/D/F): ";
            cin >> course.grade;
            if (grade_points_map.find(course.grade) != grade_points_map.end()) break;
            cout << "Invalid grade. Please enter A, B, C, D, or F.\n";
        }

        course.grade_points = course.credits * grade_points_map[course.grade];
        courses.push_back(course);
        total_credits += course.credits;
        total_grade_points += course.grade_points;
    }

    float gpa = total_grade_points / total_credits;

    cout << "\nCourse Grades:\n";
    for (const auto& course : courses) {
        cout << course.name << ": " << course.grade << " (" << course.grade_points << " grade points)\n";
    }

    cout << "\nTotal Credits: " << total_credits;
    cout << "\nTotal Grade Points: " << total_grade_points;
    cout << "\nYour GPA is: " << gpa << endl;

    return 0;
}
