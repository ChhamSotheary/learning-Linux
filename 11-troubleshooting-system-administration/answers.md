# ចម្លើយណែនាំ៖ មេរៀនទី ១១

ចម្លើយអាស្រ័យលើ incident។ គំរូវិធីគិត៖

1. កត់ពេលវេលា/timezone, URL/service និងអ្នកប្រើដែលរងផលប៉ះពាល់។
2. ពិនិត្យ uptime, memory, disk, processes និង service state ដោយ read-only commands។
3. ពិនិត្យ logs ជុំវិញពេលចាប់ផ្ដើមបញ្ហា ហើយលាក់ secrets មុនចែករំលែក។
4. ពិនិត្យ listening port, route និង DNS ដើម្បីបំបែក network symptom ពី application symptom។
5. សម្គាល់អ្វីដែលបានឃើញជាក់ស្តែងពីការសន្មត។ ឧទាហរណ៍ “service process មិនដំណើរការ” ជា fact; “disk ពេញបណ្ដាលឱ្យ service ឈប់” ជា hypothesis រហូតដល់មាន evidence។
6. មុន restart ឬកែ config ត្រូវមាន approval, impact estimate, backup និង rollback plan។
7. ក្រោយ change ត្រូវផ្ទៀងផ្ទាត់ service health និង user-facing behavior ហើយកត់លទ្ធផល។

ក្នុងសេណារីយ៉ូពិត ជំហានត្រឹមត្រូវអាចខុសគ្នាតាម runbook និងសិទ្ធិរបស់អ្នក។
