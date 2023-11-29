#include <iostream>
#include <fstream>
#include <vector>
#include <sstream>

std::vector<std::string> split(const std::string& s, char delimiter) {
    std::vector<std::string> tokens;
    std::string token;
    std::istringstream tokenStream(s);
    while (std::getline(tokenStream, token, delimiter)) {
        tokens.push_back(token);
    }
    return tokens;
}

int main() {
    std::string data;
    std::vector<std::string> lines;
    std::string filename = "data.txt";

    while (true) {
        std::cout << "Enter your data (or type 'exit' to stop): ";
        std::getline(std::cin, data);

        if (data == "exit") {
            break;
        }

        lines = split(data, ',');

        std::ofstream file(filename, std::ios_base::app);

        if (file.is_open()) {
            for (const auto& line : lines) {
                file << line << std::endl;
            }
            file << std::endl;
            file.close();
        } else {
            std::cout << "Unable to open file" << std::endl;
        }
    }

    return 0;
}
