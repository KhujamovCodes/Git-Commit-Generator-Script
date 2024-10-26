Git Commit Generator Script
Ushbu bash skripti Git repository ichida berilgan sanalar oralig'ida tasodifiy commitlar yaratadi. Quyidagi qadamlar orqali skriptni bajarishingiz mumkin.

Skriptni tayyorlash
Skriptni yaratish
Skriptni .sh kengaytmasi bilan faylga saqlang, masalan git_commit_generator.sh.

Skript tarkibi
bash
Copy code
#!/bin/bash

# Boshlanish va tugash sanalarini kiriting
start_date="2023-10-01"  # Boshlanish sana
end_date="2023-10-26"    # Tugash sana

# Commit sonlarini 1 dan 26 gacha aralashtirish
commit_counts=($(shuf -i 1-26 -n 26))

# Hozirgi sanani boshlanish sanasiga o'rnating
current_date="$start_date"

# Sana oralig'ida ishlash uchun loop
for commit_count in "${commit_counts[@]}"; do
  # Har bir kunda commit_count sonicha commit qilish
  for i in $(seq 1 $commit_count); do
    # Faylga kichik o'zgarish kiriting
    echo "Commit #$i on $current_date" > commit_file.txt

    # Gitga qo'shish
    git add commit_file.txt

    # Har bir commit uchun sanani o'zgartirib commit qilish
    GIT_COMMITTER_DATE="$current_date 12:00" git commit --date "$current_date 12:00" -m "Commit #$i on $current_date"
  done

  # Sanani 1 kunga oldinga surish
  current_date=$(date -I -d "$current_date + 1 day")
done

# O'zgartirilgan commitlarni majburiy ravishda push qilish
git push --force
Skriptni ishga tushirish
Skriptingizni bajarishdan oldin, Git repository ichida ekanligingizga ishonch hosil qiling.
Skriptingizga ijro etish huquqlarini bering:
bash
Copy code
chmod +x git_commit_generator.sh
Skriptingizni ishga tushiring:
bash
Copy code
./git_commit_generator.sh
Izohlar
start_date va end_date: Skriptda belgilangan boshlanish va tugash sanalari. Bu sanalar o'zgartirilishi mumkin.
Tasodifiy commitlar: Skript har bir kunda 1 dan 26 gacha tasodifiy commitlar yaratadi.
git push --force: Barcha o'zgartirilgan commitlarni serverga majburiy ravishda yuboradi. Diqqat, bu amaliyot boshqa commitlarni yo'qotishi mumkin, shuning uchun ehtiyotkorlik bilan foydalaning.
Foydalanish uchun tavsiyalar
Bu skript Git tarixini manipulyatsiya qiladi, shuning uchun uni ehtiyotkorlik bilan foydalaning va zarur bo'lsa, repozitoriyangizni zaxiralang.
Tasodifiy commitlar yaratish, odatda, haqiqiy loyiha ishlarida qo'llanilmaydi, lekin o'qitish va sinov uchun foydali bo'lishi mumkin.
