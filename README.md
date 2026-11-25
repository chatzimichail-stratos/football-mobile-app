# Super League Stats - User App (`football-mobile-app`)

Native Android εφαρμογή (σε Java) για φιλάθλους, η οποία προβάλλει δεδομένα του ελληνικού πρωταθλήματος **Super League**: βαθμολογία, πρόγραμμα και ζωντανή εξέλιξη αγώνων, ομαδικά και ατομικά στατιστικά, καθώς και leaderboards παικτών και ομάδων.

Αναπτύχθηκε στο πλαίσιο του μαθήματος **Ανάπτυξη Εφαρμογών για Κινητές Συσκευές (DAI210)** στο Τμήμα Εφαρμοσμένης Πληροφορικής (ΕΤΥ) του **Πανεπιστημίου Μακεδονίας** (Ιούνιος 2026).

---

## Αναφορά Έργου & Screenshots
> [!IMPORTANT]
> Για πλήρη παρουσίαση του συστήματος, περιγραφή λειτουργιών και **screenshots από τις οθόνες και των δύο Android εφαρμογών** (**User App** & **Statistic Analyst App**), δείτε την αναφορά του έργου:
>
> **[Άνοιγμα Αναφοράς & Screenshots (PDF)](docs/SuperLeagueStats_Report.pdf)**

## Πλαίσιο Έργου & Αρχιτεκτονική Οικοσυστήματος

Η εφαρμογή `football-mobile-app` αποτελεί την εφαρμογή φιλάθλων στο πλαίσιο της συνολικής εργασίας **Super League Stats**, η οποία περιλαμβάνει τρία αποθετήρια:

1. **User App (`football-mobile-app`)** - *αυτό το αποθετήριο*: Android εφαρμογή φιλάθλων για παρακολούθηση βαθμολογίας, αγώνων και στατιστικών.
2. **Statistic Analyst App ([`statistic-analyst-app`](https://github.com/FootballStats-Team1/statistic-analyst-app))**: Android εφαρμογή διαχείρισης για τον Υπεύθυνο Στατιστικής (επιλογή ενδεκάδων, καταγραφή συμβάντων αγώνα, αλλαγών και λήξης αγώνα σε πραγματικό χρόνο).
3. **Admin Web Portal ([`EPO-Portal`](https://github.com/FootballStats-Team1/EPO-Portal))**: Αυτόνομη web διεπαφή επίδειξης (demo) για δημιουργία ομάδων, παικτών, πρωταθλήματος και κλήρωση αγώνων.

> **Σημείωση:** Οι δύο Android εφαρμογές (**User App** και **Statistic Analyst App**) επικοινωνούν με κοινή βάση δεδομένων (`epodb`) μέσω των κοινών PHP Web Services (`epoDBServices`). Το **Admin Web Portal (`EPO-Portal`)** λειτουργεί αυτόνομα για σκοπούς επίδειξης και δεν συνδέεται άμεσα με την παρούσα εφαρμογή.

---

## Τεχνολογίες & Απαιτήσεις (Tech Stack)

* **Android / Build:** Java 8, `compileSdk 33`, `minSdk 24`, `targetSdk 33`, Android Gradle Plugin `7.4.0`, Gradle Wrapper `7.5` (`applicationId`: `com.example.temp_project`, `rootProject.name`: `Super League Stats`).
* **Βιβλιοθήκες Android:**
  * `OkHttp 4.9.0` (HTTP GET αιτήματα) & `org.json` (JSON parsing)
  * `Picasso 2.5.2` (φόρτωση σημάτων ομάδων και φωτογραφιών παικτών από εξωτερικά URLs)
  * `AppCompat 1.4.1`, `Material Components 1.5.0`, `ConstraintLayout 2.1.3`
* **Backend & Βάση Δεδομένων:** XAMPP (Apache HTTP Server + MariaDB/MySQL), PHP 8.x (`mysqli`), κοινά PHP Web Services (`epoDBServices`) και SQL dump (`epoDBFinalversion.sql`).

---

## Δομή Repository

```text
football-mobile-app/
├── README.md
├── docs/
│   └── SuperLeagueStats_Report.pdf          # Αναφορά έργου & screenshots (User & Analyst apps)
├── app/
│   ├── build.gradle
│   └── src/main/
│       ├── AndroidManifest.xml
│       ├── java/com/example/temp_project/   # Activities, Models, OkHttpHandler & Config
│       └── res/
│           ├── layout/                      # XML layouts οθονών & item_match.xml
│           ├── xml/                         # network_security_config.xml & backup rules
│           ├── values/                      # Προεπιλεγμένα strings, colors & themes/styles
│           ├── values-el/                   # Ελληνικά strings
│           ├── values-night/                # Night theme
│           ├── drawable*/                   # Λογότυπα (EPO, Super League) & drawables
│           └── mipmap*/                     # Εικονίδια εφαρμογής
├── phpServices_AND_sqlDump/
│   ├── epoDBFinalversion.sql                # Schema & προ-φορτωμένα δεδομένα βάσης epodb
│   └── epoDBServices/                       # Κοινά PHP Web Services (User & Analyst apps)
├── build.gradle
├── settings.gradle
└── gradle/
```

---

## Οδηγίες Εγκατάστασης & Εκτέλεσης

### 1. Προετοιμασία Περιβάλλοντος (XAMPP)
1. Εγκαταστήστε και ανοίξτε το **XAMPP Control Panel** (κατά προτίμηση **ως Διαχειριστής / Run as Administrator**).
2. Εκκινήστε τις υπηρεσίες **Apache** και **MySQL** πατώντας **Start** δίπλα σε καθεμία.

### 2. Δημιουργία & Εισαγωγή Βάσης Δεδομένων (`phpMyAdmin`)
> **Προσοχή:** Το αρχείο `epoDBFinalversion.sql` περιέχει μόνο τους ορισμούς και τα δεδομένα των πινάκων (χωρίς εντολές `CREATE DATABASE` / `USE`). Συνεπώς, πρέπει πρώτα να δημιουργήσετε και να επιλέξετε τη βάση `epodb` πριν την εισαγωγή.

1. Ανοίξτε στον browser τη διεύθυνση `http://localhost/phpmyadmin/`.
2. *(Προαιρετικά)* Αν υπάρχει παλαιότερη βάση `epodb`, διαγράψτε την (**Drop**) για να αποφύγετε διενέξεις.
3. Δημιουργήστε νέα βάση δεδομένων με όνομα **`epodb`** και κωδικοποίηση `utf8mb4_general_ci`.
4. Επιλέξτε τη βάση **`epodb`** από την αριστερή στήλη, μεταβείτε στην καρτέλα **Εισαγωγή (Import)**, επιλέξτε το αρχείο `phpServices_AND_sqlDump/epoDBFinalversion.sql` και πατήστε **Εκτέλεση / Import**.
5. Θα δημιουργηθούν οι 5 πίνακες (`matches`, `match_events`, `match_lineups`, `players`, `teams`) με προ-φορτωμένα δεδομένα πρωταθλήματος (10 ομάδες, 9 αγωνιστικές: αγωνιστικές 1–3 `finished`, αγωνιστική 4 `live`, αγωνιστικές 5–9 `pending`).

### 3. Τοποθέτηση PHP Web Services
1. Αντιγράψτε ολόκληρο τον φάκελο `phpServices_AND_sqlDump/epoDBServices/` μέσα στον κατάλογο `htdocs` του XAMPP (συνήθως `C:\xampp\htdocs\epoDBServices`).

### 4. Ρύθμιση IP στην Android Εφαρμογή
1. Βρείτε την τοπική **IPv4** διεύθυνση του υπολογιστή σας (π.χ. μέσω `ipconfig`, όπως `192.168.1.xxx`).
2. Ανοίξτε το αρχείο `app/src/main/java/com/example/temp_project/Config.java` και ενημερώστε τη σταθερά `IP`:
   ```java
   public static final String IP = "192.168.1.xxx";
   public static final String BASE_URL = "http://" + IP + "/epoDBServices/";
   ```
3. Ανοίξτε το `app/src/main/res/xml/network_security_config.xml` και ενημερώστε το `<domain>` με την ίδια IP ώστε να επιτρέπεται η HTTP (cleartext) κίνηση.

### 5. Εκτέλεση Εφαρμογής
1. Ανοίξτε το project στο **Android Studio** και εκτελέστε Gradle Sync.
2. Εκτελέστε το module `:app` σε Android Emulator ή φυσική συσκευή (API 24+) συνδεδεμένη στο ίδιο τοπικό δίκτυο με τον XAMPP server (βεβαιωθείτε ότι το firewall επιτρέπει εισερχόμενη κίνηση στη θύρα 80 του Apache και ότι η συσκευή έχει πρόσβαση στο διαδίκτυο για τη φόρτωση σημάτων/φωτογραφιών μέσω Picasso).

---

## Οθόνες & Ροή Πλοήγησης

```text
MainActivity
  └─ AppMenuActivity
       ├─ StandingsActivity
       ├─ MatchesActivity
       │    └─ MatchDetailsActivity          [MATCH_ID]
       │         └─ PersonalStatsActivity    [PLAYER_NAME, MATCH_ID]
       └─ TopStatsActivity
```

* **`MainActivity` (`activity_main.xml`):** Αρχική οθόνη με λογότυπο ΕΠΟ, κουμπί οδηγιών (`?`), εναλλαγή γλώσσας (`EN/GR`) και είσοδο στην υπηρεσία (`Enter Service` / `Είσοδος στην Υπηρεσία`).
* **`AppMenuActivity` (`activity_app_menu.xml`):** Κεντρικό μενού με πρόσβαση σε Βαθμολογία, Αγώνες και Τοπ Στατιστικά.
* **`StandingsActivity` (`activity_standings.xml`):** Δυναμικός πίνακας βαθμολογίας (`#`, Σήμα, `TEAM`, `MP`, `GD`, `PTS`) που υπολογίζεται on-the-fly από τους ολοκληρωμένους αγώνες (`status='finished'`). Οι 2 τελευταίες θέσεις επισημαίνονται με κόκκινο φόντο (ζώνη υποβιβασμού).
* **`MatchesActivity` (`activity_matches.xml`):** Επιλογή αγωνιστικής (1–9) μέσω Spinner και προβολή καρτών αγώνων (`item_match.xml`) με διάκριση `live` (κόκκινο σκορ με ένδειξη `Live`), `pending` (`- : -`) και `finished`.
* **`MatchDetailsActivity` (`activity_match_details.xml`):** Προβολή κεφαλίδας αγώνα (σήματα, σκορ, κατάσταση) και δύο καρτέλες:
  * **TEAM STATS:** Κατοχή μπάλας (υπολογισμένη από τις πάσες), συνολικά σουτ, σουτ εντός εστίας, πάσες, ευστοχία πάσας, επιτυχημένα τάκλιν, κόρνερ, φάουλ, κίτρινες και κόκκινες κάρτες.
  * **PERSONAL STATS:** Επιλογέας ομάδας (γηπεδούχος/φιλοξενούμενος) για προβολή βασικών (`Starting`) και αναπληρωματικών (`Substitutes`) με χρωματική κωδικοποίηση κατάστασης (κόκκινο = κόκκινη κάρτα, πράσινο = συμμετοχή σε αλλαγή — είσοδος ή έξοδος, κίτρινο = κίτρινη κάρτα, προτεραιότητα: `red > green > yellow`). Πατώντας έναν παίκτη ανοίγουν τα ατομικά στατιστικά του.
* **`PersonalStatsActivity` (`activity_personal_stats.xml`):** Φωτογραφία και 15 αναλυτικά ατομικά στατιστικά του επιλεγμένου παίκτη για τον συγκεκριμένο αγώνα (γκολ, ασίστ, σουτ εντός/εκτός, εύστοχες/άστοχες πάσες, τάκλιν, σέντρες, λάθη, κερδισμένα/διαπραχθέντα φάουλ, κίτρινες και κόκκινες κάρτες).
* **`TopStatsActivity` (`activity_top_stats.xml`):** Εναλλαγή μεταξύ ατομικών (`Personal`) και ομαδικών (`Team Stats`) κατατάξεων (Leaderboards) σε Γκολ, Ασίστ, Κίτρινες και Κόκκινες κάρτες.

---

## Επικοινωνία με Backend (API Endpoints)

Όλες οι κλήσεις από το User App εκτελούνται μέσω **HTTP GET** προς το `Config.BASE_URL` και επιστρέφουν JSON:

| Endpoint | Παράμετροι | Περιγραφή |
| :--- | :--- | :--- |
| `getStandings.php` | — | Υπολογίζει και επιστρέφει δυναμικά τη βαθμολογία από αγώνες με `status='finished'`. |
| `getMatches.php` | `matchday` *(προεπ. `1`)* | Επιστρέφει τους αγώνες της επιλεγμένης αγωνιστικής (σκορ `-1` για `pending`). |
| `getMatchDetails.php` | `matchId` | Επιστρέφει στοιχεία αγώνα και συγκεντρωτικά `home_stats` / `away_stats` (με κατοχή & κόρνερ). |
| `getMatchLineups.php` | `matchId` | Επιστρέφει `home_starters`, `away_starters`, `home_subs`, `away_subs`. |
| `getLineupStatus.php` | `matchId` | Επιστρέφει το χρώμα κατάστασης (`red`, `green`, `yellow` ή `""`) ανά παίκτη. |
| `getMatchPlayerStats.php` | `matchId` | Επιστρέφει τα ατομικά στατιστικά των παικτών (`home_players`, `away_players`). |
| `getTopStats.php` | `stat`, *(προαιρ. `limit`, προεπ. `7`)* | Κορυφαίοι παίκτες (`goals`, `assists`, `yellow_cards`, `red_cards`). |
| `getTeamTopStats.php` | `stat` | Κατάταξη ομάδων ανά κατηγορία στατιστικού (χρησιμοποιούνται `goals`, `assists`, `yellow_cards`, `red_cards`). |

> **Σημείωση για τα υπόλοιπα PHP scripts:** Ο φάκελος `phpServices_AND_sqlDump/epoDBServices/` περιλαμβάνει το πλήρες κοινό σύνολο των 17 Web Services. Τα υπόλοιπα 9 endpoints (`saveLineups.php`, `insertMatchEvent.php`, `insertSubstitution.php`, `updateMatchStatus.php`, `checkLineup.php`, `getMatchPlayers.php`, `getPlayersForAnalyst.php`, `getMatchdayStatus.php`, `getPlayerStats.php`) εξυπηρετούν κυρίως το **Statistic Analyst App** ή αποτελούν βοηθητικές υπηρεσίες.

---

## Βάση Δεδομένων & Σχέσεις

Η βάση δεδομένων `epodb` περιλαμβάνει 5 πίνακες:

* `teams` - Ομάδες, πόλη και URL σήματος (`badge`)
* `players` - Παίκτες, θέση, URL φωτογραφίας (`photo`) και συσχέτιση με ομάδα (`team_id`)
* `matches` - Αγωνιστικές, γηπεδούχος/φιλοξενούμενος, κατάσταση (`pending`/`live`/`finished`), σκορ και ομαδικά κόρνερ (`home_corners`, `away_corners`)
* `match_lineups` - Αρχική ενδεκάδα/πάγκος (`is_starting`) και τρέχουσα παρουσία στον αγωνιστικό χώρο (`is_on_pitch`) ανά αγώνα
* `match_events` - Συγκεντρωτικά ατομικά στατιστικά ανά παίκτη και αγώνα (με `UNIQUE KEY (match_id, player_id)`)

```text
teams 1 ─── n players
teams 1 ─── n matches (ως home_team_id ή away_team_id)
matches 1 ─── n match_lineups
matches 1 ─── n match_events
players 1 ─── n match_lineups
players 1 ─── n match_events
```

---

## Γνωστοί Περιορισμοί & Παρατηρήσεις

* **Τοπικό Δίκτυο & Ασφάλεια (μόνο για τοπική χρήση):** Η IP είναι hardcoded στο `Config.java` και στο `network_security_config.xml`, επιτρέπεται cleartext HTTP κίνηση (`usesCleartextTraffic="true"`), δεν υπάρχει authentication και τα PHP scripts συνδέονται στη MariaDB ως `root` χωρίς password.
* **Δικτυακές Κλήσεις στο UI Thread:** Ο `OkHttpHandler` ενεργοποιεί `StrictMode.permitAll()` εκτελώντας σύγχρονα HTTP αιτήματα στο main thread, ενώ τα `TopStatsList`, `TeamTopStatsList` και `MatchDetailsActivity.fetchPlayerColors()` ξεκινούν worker thread αλλά καλούν άμεσα `Thread.join()`, μπλοκάροντας το UI thread μέχρι την απόκριση.
* **Εναλλαγή Γλώσσας (`EN/GR`) & Hardcoded Labels:** Η αλλαγή locale εφαρμόζεται προσωρινά με `recreate()` χωρίς μόνιμη αποθήκευση. Ορισμένα κείμενα (π.χ. οι τίτλοι/επικεφαλίδες στο `TopStatsActivity` και η ένδειξη `"LIVE"` στο `MatchDetailsActivity`) παραμένουν hardcoded.
* **Αγωνιστικές:** Το `MatchesActivity` ορίζει σταθερά 9 αγωνιστικές στον κώδικα και επισημαίνει στατικά την 4η αγωνιστική (index `3`) με κόκκινο χρώμα στη λίστα του Spinner.
* **Αναγνώριση Παίκτη:** Η πλοήγηση προς `PersonalStatsActivity` μεταφέρει το `PLAYER_NAME` αντί για μοναδικό `player_id` και αναζητά τον παίκτη με αντιστοίχιση ονόματος.
* **Legacy Στοιχεία:** Υπάρχουν ορισμένα αχρησιμοποίητα/legacy στοιχεία από την αρχική ενιαία σχεδίαση πριν τον διαχωρισμό των δύο Android εφαρμογών (π.χ. κλάσεις `User.java`, `Player.java`, `app_name = temp-project`, και αναφορά επιλογής ρόλου στο κείμενο του dialog οδηγιών της `MainActivity`).

---

## Ομάδα Ανάπτυξης (Ομάδα 1)

**Διδάσκοντες:** Αμπατζόγλου Απόστολος, Τρακατέλης Γεώργιος

| Ονοματεπώνυμο | ΑΕΜ |
| :--- | :--- |
| Παπαδόπουλος Δημήτριος | ics24004 |
| Μαυρομάτης Αχιλλέας | ics24095 |
| Καραγέλης Κωνσταντίνος | ics24102 |
| Χατζημιχαήλ Ευστράτιος | ics24204 |
| Γιαννούδης Χρήστος | ics24052 |
