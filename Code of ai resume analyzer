#include <ctype.h>
#include <stdio.h>
#include <string.h>

#define SKILL_COUNT 28
#define SECTION_COUNT 6
#define MAX_TEXT 12000

static const char *ALL_SKILLS[SKILL_COUNT] = {
    "python", "java", "c++", "javascript", "sql", "html", "css",
    "react", "flask", "django", "node.js", "rest api",
    "machine learning", "deep learning", "nlp", "tensorflow", "pytorch",
    "scikit-learn", "pandas", "numpy", "computer vision", "git",
    "docker", "aws", "linux", "mongodb", "mysql", "power bi"
};

static const char *SECTIONS[SECTION_COUNT] = {
    "education", "experience", "projects",
    "skills", "certifications", "summary"
};

void normalize_text(const char *src, char *dst) {
    int i;

    for (i = 0; src[i] && i < MAX_TEXT - 1; ++i) {
        unsigned char c = (unsigned char)src[i];

        dst[i] = (isalnum(c) || c == '+' || c == '#' || c == '.')
            ? (char)tolower(c)
            : ' ';
    }

    dst[i] = '\0';
}

int contains_skill(const char *text, const char *skill) {
    char clean[MAX_TEXT];
    char query[128];
    char padded[MAX_TEXT + 3];
    char pattern[132];

    normalize_text(text, clean);
    normalize_text(skill, query);

    snprintf(padded, sizeof(padded), " %s ", clean);
    snprintf(pattern, sizeof(pattern), " %s ", query);

    return strstr(padded, pattern) != NULL;
}

int find_skills(const char *text, int found[]) {
    int i;
    int count = 0;

    for (i = 0; i < SKILL_COUNT; ++i) {
        found[i] = contains_skill(text, ALL_SKILLS[i]);
        count += found[i];
    }

    return count;
}

int detect_sections(const char *text, int found[]) {
    char clean[MAX_TEXT];
    int i;
    int count = 0;

    normalize_text(text, clean);

    for (i = 0; i < SECTION_COUNT; ++i) {
        found[i] = strstr(clean, SECTIONS[i]) != NULL;
        count += found[i];
    }

    return count;
}
