ශ්‍රී සුගත විවේක සේනාසනය – දායක සභා පද්ධතිය (Cloud Sync)

මෙම ZIP එක Android Studio ව්‍යාපෘතිය සහ ලැප්ටොප්/ෆෝන් දෙකෙන්ම භාවිත කළ හැකි Firebase Hosting වෙබ් යෙදුම අඩංගු මූලාශ්‍ර ගොනුවකි. මෙය සූදානම් APK එකක් හෝ සජීවීව ප්‍රකාශිත වෙබ් අඩවියක් නොවේ.

ඇතුළත් ප්‍රධාන කොටස්:
- ඉඩම් අංකයෙන් දායකයා සෙවීම
- දායක තොරතුරු එකතු කිරීම / සංස්කරණය / මකා දැමීම
- සාමාන්‍ය සහ පොහොය දින දාන භාරගැනීම් ඇතුළත් කිරීම
- CSV සහ JSON Backup පහසුකම්
- ඊමේල් + මුරපද පිවිසුම
- Firebase Cloud Firestore හරහා ෆෝන් සහ ලැප්ටොප් අතර සජීවී දත්ත සමමුහුර්තකරණය
- Android ඇප් එකේ biometric තහවුරු කිරීම තවදුරටත් අමතර ආරක්ෂාවක් ලෙස පවතී
- “ඉදිරි දාන භාරගැනීම් / සටහන්” ලැයිස්තු කොටස ඉවත් කර ඇත; දාන ඇතුළත් කිරීමේ පෝරමය පවතී.

වැදගත්:
Firebase ව්‍යාපෘතියක් සාදා සැකසුම් ඇතුළත් කර Hosting deploy කරන තුරු Cloud login ක්‍රියා නොකරයි. මෙම ව්‍යාපෘතිය ඔබගේ Firebase ගිණුමට සම්බන්ධ කර deploy කළ යුතුය.

1. Firebase ව්‍යාපෘතිය සකස් කිරීම
- https://console.firebase.google.com වෙත ගොස් නව project එකක් සාදන්න.
- Authentication > Sign-in method තුළ Email/Password සක්‍රීය කරන්න.
- Authentication > Users තුළ පරිපාලක ගිණුමක් Add user මඟින් සාදන්න. මහජන Sign up එකක් යෙදුමේ නැත.
- Firestore Database එකක් සාදන්න. ඇප් එක දත්ත users/{ඔබගේ UID}/donors සහ users/{ඔබගේ UID}/donations යටතේ ගබඩා කරයි; dayakas නමින් වෙනම collection එකක් භාවිත නොකරයි. එබැවින් dayakas/test පරීක්ෂණ ලේඛනය ඇප් එකට අවශ්‍ය නොවේ.
- Project settings > Your apps > Web app එකක් එක් කර Firebase config අගයන් ලබාගන්න.

2. Firebase config ඇතුළත් කිරීම
- ඔබ ලබාදුන් Firebase Web App සැකසුම් app/src/main/assets/firebase-config.js සහ hosting/firebase-config.js ගොනු දෙකෙහිම දැනට ඇතුළත් කර ඇත. වෙනස් කිරීමක් අවශ්‍ය නැත.

3. Firestore ආරක්ෂක නීති
- Firebase Console > Firestore Database > Rules තුළ firestore.rules ගොනුවේ අන්තර්ගතය යොදන්න.
- නීති අනුව ලොග් වූ පරිශීලකයාට තමන්ගේ users/{uid} යටතේ ඇති දත්ත පමණක් කියවීමට/ලියීමට හැකිය.

4. Firebase Hosting deploy කිරීම
- පරිගණකයේ Node.js සහ Firebase CLI ස්ථාපනය කරන්න.
- මෙම project folder එක තුළ terminal එකක් විවෘත කර:
  npm install -g firebase-tools
  firebase login
  firebase use --add
  firebase deploy
- firebase use --add අවස්ථාවේ ඔබ සෑදූ Firebase project එක තෝරන්න.
- Deploy වූ පසු https://YOUR_PROJECT_ID.web.app වැනි වෙබ් ලිපිනයක් ලැබේ. එය ෆෝන් සහ ලැප්ටොප් දෙකෙන්ම විවෘත කරන්න.

5. Android APK සෑදීම
- app/src/main/java/lk/sugatha/dayaka/MainActivity.kt ගොනුවේ YOUR_FIREBASE_PROJECT_ID යන්න ඔබගේ Firebase project ID එකෙන් මාරු කරන්න.
- Android Studio තුළ project එක Open කර Gradle Sync කරන්න.
- Build > Build Bundle(s) / APK(s) > Build APK(s) තෝරන්න.
- Firebase Hosting URL එක load වන APK එක build කරන්න.
- Android app එකේ biometric තහවුරු කිරීමෙන් පසු Firebase ඊමේල්/මුරපදයෙන්ද පිවිසිය යුතුය.

පැරණි දත්ත:
- පැරණි localStorage දත්ත පළමු සාර්ථක login එකේදී Firestore වෙත එක් කිරීමට migration ක්‍රමයක් ඇතුළත් කර ඇත.
- දැනටමත් Firestore තුළ දත්ත තිබේ නම්, අලුත් දත්ත ID අනුව පමණක් එක් කරයි.
- පැරණි දත්ත කිසිවක් මකා නොදමන්න. Deploy කිරීමට පෙර මුල් දත්ත backup එකක් තබාගන්න.

ආරක්ෂාව:
- Firebase config තුළ ඇති apiKey යනු client configuration එකකි; Firestore Rules තමයි දත්ත ප්‍රවේශය පාලනය කරන්නේ.
- මුරපදය කිසිවිටෙක කේත ගොනුවක ලියන්න එපා.
- Firebase Console තුළ ශක්තිමත් මුරපදයක් යොදා පරිපාලක ගිණුම සාදන්න.
- මෙම project source එක මෙහිදී Firebase account එකකට deploy කර නැති අතර සැබෑ Firebase config නොමැති බැවින් සජීවී cloud sync තවම ක්‍රියාත්මක කර නැත.
