profile/README.md ma wspierać moje CV (plik cv.md) i trafiać głównie do rekruterów (w tym z UK), warto pomyśleć o tym README jak o "wizytówce dla rekrutera skanującego w 15 sekund", a nie jak o dokumentacji technicznej. Kluczowe elementy:

**1. Krótkie "kim jestem"**
- Rola, stack, ew. czego aktualnie szukasz (skoro jesteś w trakcie rekrutacji)
- Link do CV, LinkedIn, maila — najważniejsze, żeby rekruter mógł od razu przejść dalej

**2. Sekcja z projektami — nie lista repo, tylko "co to pokazuje"**
Dla każdego projektu krótko:
- Co robi (1-2 zdania)
- Stack technologiczny (badge'y albo tabelka)
- **Jaką umiejętność/koncept demonstruje** — to jest najważniejsze dla rekrutera. Np. przy `coupon-service` warto podkreślić: reactive/WebFlux, atomowość pod concurrency, projektowanie API, testy z Testcontainers + próg pokrycia. To są konkretne, "sprzedające" hasła, których szuka osoba przeglądająca CV.
- Link do repo (i do demo, jeśli jakieś jest)

**3. Ogólny stack / umiejętności**
Zbiorcze badge'y (Java, Spring Boot, PostgreSQL, Docker itd.) — rekruterzy czasem skanują wzrokiem po badge'ach zanim przeczytają tekst.

**4. Kontekst organizacji**
Jedno zdanie wyjaśniające, że to zbiór przykładowych/rekrutacyjnych projektów (skoro repo już teraz wspomina, że `coupon-service` to implementacja konkretnego zadania rekrutacyjnego) — warto to uczciwie zaznaczyć, żeby nie wyglądało na produkcyjny projekt firmy.

**5. Kontakt na końcu**
Powtórzony link do LinkedIn/maila — rekruterzy często szukają go na końcu, jeśli przewinęli całość.

Kilka dodatkowych wskazówek:
- Skoro odzywają się głównie rekruterzy z UK, rozważ README po angielsku (albo dwujęzyczne, ale to zwykle się rozjeżdża).
- Nie przesadzaj z długością — to ma być "landing page", a nie dokumentacja. Szczegóły techniczne zostaw w README poszczególnych repo (jak w `coupon-service`, które już jest bardzo solidne).
- Jeśli `skill-flip` ma jakiś link do demo (GitHub Pages?), koniecznie go dodaj — działający link jest dużo mocniejszy niż sam kod.
- `coupon-service` -> /Users/bartek/Documents/Projects/AiB/rekrutacje/empik-coupon-service
- `skill-flip` -> /Users/bartek/Documents/Projects/AiB/rekrutacje/Skill Flip
- linkedin.com/in/bartekmarciniak
