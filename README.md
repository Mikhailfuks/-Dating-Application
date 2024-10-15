#include <iostream>
#include <vector>
#include <string>

class Profile {
public:
    Profile(const std::string& name, int age, const std::string& interests)
        : name(name), age(age), interests(interests) {}

    void displayProfile() const {
        std::cout << "Name: " << name << ", Age: " << age << ", Interests: " << interests << std::endl;
    }

    int getAge() const {
        return age;
    }

    const std::string& getName() const {
        return name;
    }

private:
    std::string name;
    int age;
    std::string interests;
};

class DatingApp {
public:
    void createProfile() {
        std::string name;
        int age;
        std::string interests;

        std::cout << "Enter your name: ";
        std::cin >> ws; // Discard leading whitespace
        std::getline(std::cin, name);
        std::cout << "Enter your age: ";
        std::cin >> age;
        std::cout << "Enter your interests: ";
        std::cin >> ws; // Discard leading whitespace
        std::getline(std::cin, interests);

        profiles.push_back(Profile(name, age, interests));
        std::cout << "Profile created successfully!" << std::endl;
    }

    void listProfiles() const {
        std::cout << "\n--- List of Profiles ---" << std::endl;
        for (const auto& profile : profiles) {
            profile.displayProfile();
        }
    }

    void findMatch(int age) const {
        std::cout << "\n--- Potential Matches ---" << std::endl;
        for (const auto& profile : profiles) {
            if (profile.getAge() == age) { // Simple matching criterion by age
                std::cout << "Match found: ";
                profile.displayProfile();
            }
        }
    }

private:
    std::vector<Profile> profiles;
};

int main() {
    DatingApp app;
    int choice;

    do {
        std::cout << "\n=== Dating Application ===" << std::endl;
        std::cout << "1. Create Profile" << std::endl;
        std::cout << "2. List Profiles" << std::endl;
        std::cout << "3. Find Match" << std::endl;
        std::cout << "4. Exit" << std::endl;
        std::cout << "Enter your choice: ";
        std::cin >> choice;

        switch (choice) {
            case 1:
                app.createProfile();
                break;
            case 2:
                app.listProfiles();
                break;
            case 3: {
                int age;
                std::cout << "Enter age to find matches: ";
                std::cin >> age;
                app.findMatch(age);
                break;
            }
            case 4:
                std::cout << "Exiting..." << std::endl;
                break;
            default:
                std::cout << "Invalid choice! Please try again." << std::endl;
        }
    } while (choice != 4);

    return 0;
}
