#include <stdio.h>
#include <stdlib.h>

int main(int argc, char *argv[]) {
	if (argc != 2) {
		printf("Please provide a file to read from!\n");
		return 1;
	}
	
	char CONT[1000];

	char ch;
	FILE *fp;
	fp = fopen(argv[1], "r");
	if (fp == NULL) {
		perror("Error when opening file\n");
		exit(EXIT_FAILURE);
	}

	fseek(fp, 0, SEEK_END);
	int size = ftell(fp);
	fseek(fp, 0, SEEK_SET);
	if (size > 1000) {
		printf("File is too big!");
		return 1;
	}
	
	int IS_ITALIC = 0; // 1 for true, 0 for false
	int IS_BOLD = 0;
	char LAST_CHAR;

	while ((ch = fgetc(fp)) != EOF) { // Read char by char from fil
		if (ch == '*') {
			if (LAST_CHAR == '*') {
				if (IS_BOLD == 1) {
					fflush(stdout);
					printf("\b\b\b\b</strong>");
					IS_BOLD = 0;
					LAST_CHAR = '*';
					continue;
				}
				fflush(stdout);
				printf("\b\b\b<strong>");
				IS_BOLD = 1;
				LAST_CHAR = '*';
				continue;
			}

			if (IS_ITALIC == 1) {
				printf("</i>");
				IS_ITALIC = 0;
				LAST_CHAR = '*';
				continue;
			}
			printf("<i>");
			IS_ITALIC = 1;
			LAST_CHAR = '*';
			continue;			
		}

		printf("%c", ch);
		LAST_CHAR = ch;
	}

	fclose(fp);
	return 0;
}
