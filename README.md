# temps
jour et nuit temps réel
#include <iostream>
#include <ctime> // pour la fonction time
#include <chrono> // pour la fonction sleep

int main() {
    // Boucle infinie pour simuler l'animation du jour et de la nuit
    while (true) {
        // Obtient le temps actuel en secondes
        time_t now = time(nullptr);

        // Calcule le nombre de secondes depuis minuit
        struct tm* midnight = localtime(&now);
        midnight->tm_hour = 0;
        midnight->tm_min = 0;
        midnight->tm_sec = 0;
        time_t midnight_time = mktime(midnight);
        int seconds_since_midnight = difftime(now, midnight_time);

        // Détermine si c'est le jour ou la nuit en fonction du temps actuel
        bool is_daytime = (seconds_since_midnight >= 6 * 60 * 60 && seconds_since_midnight < 18 * 60 * 60);

        // Affiche le message approprié en fonction du moment de la journée
        if (is_daytime) {
            std::cout << "Le soleil brille !" << std::endl;
        } else {
            std::cout << "La lune est visible." << std::endl;
        }

        // Fait une pause de 5 secondes avant la prochaine étape de l'animation
        std::this_thread::sleep_for(std::chrono::seconds(5));
    }

    return 0;
}
