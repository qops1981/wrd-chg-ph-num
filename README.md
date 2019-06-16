# Interview Homework
## William R DeLuca

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
    sed -r "s/[1\(. 1]*800[\) -.]*(438|GET)[- .]*(4357|HELP)/202-456-1414/g" ${BU_PATH} > ${OG_PATH}; \
    chmod --reference ${BU_PATH} ${OG_PATH}; \
done; echo
```
