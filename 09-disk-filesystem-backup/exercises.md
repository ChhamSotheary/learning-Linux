# លំហាត់មេរៀនទី ៩៖ Disk, Filesystem និង Backup

## ផ្នែក A៖ សំណួរ

1. Disk, partition, filesystem និង mount point ខុសគ្នាដូចម្តេច?
2. df និង du បង្ហាញព័ត៌មានខុសគ្នាយ៉ាងណា?
3. ហេតុអ្វីត្រូវពិនិត្យ archive contents មុន restore archive មិនស្គាល់?
4. តើហេតុអ្វីត្រូវសាក restore backup?
5. តើ commands mkfs និង dd មានហានិភ័យអ្វី?

## ផ្នែក B៖ អនុវត្ត Backup/Restore

~~~bash
mkdir -p "$HOME/linux-practice/exercise-09/source"
mkdir -p "$HOME/linux-practice/exercise-09/backups"
mkdir -p "$HOME/linux-practice/exercise-09/restored"
printf '%s\n' "Test data" > "$HOME/linux-practice/exercise-09/source/test.txt"
tar -czf "$HOME/linux-practice/exercise-09/backups/test.tar.gz" -C "$HOME/linux-practice/exercise-09/source" .
tar -tzf "$HOME/linux-practice/exercise-09/backups/test.tar.gz"
tar -xzf "$HOME/linux-practice/exercise-09/backups/test.tar.gz" -C "$HOME/linux-practice/exercise-09/restored"
cat "$HOME/linux-practice/exercise-09/restored/test.txt"
~~~

កត់លទ្ធផល df -h និង lsblk -f របស់ម៉ាស៊ីន។ កុំប្រើ partition/format commands។

## លក្ខខណ្ឌបញ្ចប់

- អាចបង្កើត និងផ្ទៀងផ្ទាត់ archive។
- អាច restore archive ទៅថតថ្មី។
- អាចពន្យល់ថាហេតុអ្វី restore testing ចាំបាច់។
- មិនកែ partitions ឬ format disks ពិត។
