# មេរៀនទី ២៖ Logs, Journal និង Retention

systemd-journald ប្រមូល log ពី service និង kernel ហើយអាចរក្សាទុកជា volatile ក្នុង /run ឬ persistent នៅ /var/log/journal អាស្រ័យលើ configuration។ កុំសន្មតថា log នឹងនៅក្រោយ reboot; ពិនិត្យ config និង test តាមគោលការណ៍របស់អ្នក។

~~~bash
journalctl --disk-usage
journalctl --list-boots
journalctl -b -u ssh --since today --no-pager
~~~

Log rotation/retention ត្រូវមានកំណត់ត្រាតាមទំហំ និងពេលវេលា។ សូមគោរព privacy និងកុំទុក password/token ក្នុង log។ ការកែ journald.conf ត្រូវសាកល្បង និងរៀបចំ rollback។

## លំហាត់

កំណត់ប្រភព log សម្រាប់ kernel, system service និង application មួយ។ សរសេរថា log រក្សាទុកទីណា, រយៈពេលប៉ុន្មាន, អ្នកណាអាចអាន និងរបៀបរក្សាភស្តុតាងដោយមិនបង្ហោះជាសាធារណៈ។
