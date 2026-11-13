# ចម្លើយណែនាំ៖ មេរៀនទី ៥

## ផ្នែក A

1. Package ជាបណ្ដុំកម្មវិធី/ឯកសារ និង metadata ដែល package manager អាចគ្រប់គ្រង។ Repository ជាប្រភព packages។
2. apt update refreshes local repository metadata។ apt upgrade ដំឡើងកំណែថ្មីរបស់ packages តាម metadata ដែលមាន។ វាជាសកម្មភាពខុសគ្នា។
3. Fedora ប្រើ DNF ជាទូទៅ; Arch Linux ប្រើ pacman។ Ubuntu/Debian ប្រើ APT។
4. Transaction summary បង្ហាញ packages ដែលនឹងដំឡើង កែ ឬដកចេញ ដើម្បីឱ្យអ្នកឃើញផលប៉ះពាល់មុន confirm។
5. Signature verification ជួយពិនិត្យភាពត្រឹមត្រូវ/ប្រភព package។ ការបិទវាអាចឱ្យ package មិនទុកចិត្តបានត្រូវបានដំឡើង។

## ផ្នែក B

លទ្ធផល version/repository អាស្រ័យលើ distro និងពេលដែលរត់ command។ ចម្លើយត្រូវកត់ត្រាអ្វីដែលម៉ាស៊ីនរបស់អ្នកបង្ហាញពិត។

## ផ្នែក C

ពិនិត្យអ្នកថែទាំ និង domain របស់ repository, signing key/fingerprint, package provenance, permissions ដែល script ត្រូវការ, commands ដែលនឹងរត់, dependencies និង recovery plan។ សាកល្បងក្នុង VM/staging ហើយកុំដំណើរការ script ដោយ root ប្រសិនបើមិនយល់ពីវា។
