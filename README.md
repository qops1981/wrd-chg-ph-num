# Interview Homework (Phone Number Change)
#### William DeLuca

### Gem Dependencies
* `rake`

### Pipeline Bash Script
The following script written in bash can be copy and pasted into the terminal to perform the phone number alterations.
```bash
COUNTER=1; \
echo "Make Backup Directory"; \
mkdir -p /tmp/backup; \
echo "Backing Up HTML Files"; \
cp -a /tmp/var/www /tmp/backup; \
echo "Modify Production Files"; \
ls -1 /tmp/backup/www | while read file; do \
    BU_PATH="/tmp/backup/www/${file}"; \
    OG_PATH="/tmp/var/www/${file}"; \
    printf "\rModifying: %s %d" ${OG_PATH} $((COUNTER++)); \
    sed -r "s/[1\(. -]*800[\) -.]*(438|GET)[- .]*(4357|HELP)/202-456-1414/g" ${BU_PATH} > ${OG_PATH}; \
    chmod --reference ${BU_PATH} ${OG_PATH}; \
done; echo
```
### Testing Setup
#### Rake
Setup `/tmp/var/www` and fill will sample HTML files
#### Rake Clean
Delete all HTML from `/tmp/var/www` and `/tmp/backup/www`
#### Rake Clobber
Delete all HTML from `/tmp/var/www` and `/tmp/backup/www` and delete the `/tmp/var` and `/tmp/backup` directories