# មេរៀនទី ៤៖ Change Management និង Runbook

ការផ្លាស់ប្តូរ kernel, network, storage, firewall ឬ systemd អាចបង្កផលប៉ះពាល់ធំ។ Change plan គួរមាន scope, owner, evidence, pre-check, maintenance window, success signal និង rollback ដែលបានសាកល្បង។ ការអនុម័ត និងលំដាប់ការងារត្រូវធ្វើតាមគោលការណ៍អង្គភាព។

## គំរូ runbook

1. រោគសញ្ញា និងផលប៉ះពាល់។
2. សិទ្ធិ/អ្នកទទួលខុសត្រូវ និងពេលវេលាដែលអាចធ្វើ។
3. Pre-check និង snapshot/backup។
4. ជំហានតូចៗមួយៗ និង command ច្បាស់លាស់។
5. សញ្ញាជោគជ័យ និងសញ្ញាឈប់។
6. Rollback, verification និងកំណត់ហេតុក្រោយ incident។

## លំហាត់

សរសេរ runbook ប្តូរ configuration តូចមួយក្នុង VM ផ្ទាល់ខ្លួន។ បន្ថែម test និង rollback ហើយឱ្យអ្នកដទៃអាចអនុវត្តតាមដោយមិនបកស្រាយផ្ទាល់មាត់។
