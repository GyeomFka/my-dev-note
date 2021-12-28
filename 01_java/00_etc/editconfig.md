### .editorconfig 파일 설정
`.editorconfig` 는 다양한 에디터와 IDE에서 공통적으로 지원하는 코드 스타일에 대한 설정 파일이다. 자세한 스펙은 https://editorconfig.org/ 에서 파악할 수 있다. 다양한 에디터로 파일을 고칠 때 같은 규칙을 참조할수 있도록 가급적 이 파일을 소스 저장소에서 올려서 공유하는 것을 권장한다.

`.editconfig`의 예제
```editorconfig
# top-most EditorConfig file
root = true

[*]
# [encoding-utf8]
charset = utf-8

# [newline-lf]
end_of_line = lf

# [newline-eof]
insert_final_newline = true

[*.bat]
end_of_line = crlf

[*.java]
# [indentation-tab]
indent_style = tab

# [4-spaces-tab]
indent_size = 4
tab_width = 4

# [no-trailing-spaces]
trim_trailing_whitespace = true

[line-length-120]
max_line_length = 120
```

### Gradle 설정
```groovy
plugins {
    id 'java'
}

//...

// 방법1
compileJava.options.encoding = 'UTF-8'
compileTestJava.options.encoding = 'UTF-8'

// 방법 2
[compileJava, compileTestJava]*.options*.encoding = 'UTF-8'

// 방법 3
tasks.withType(Compile) {
    options.encoding = 'UTF-8'
}
```

### IntelliJ Formatter 적용
- [formatter.xml](https://github.com/naver/hackday-conventions-java/blob/master/rule-config/naver-intellij-formatter.xml)
    - naver-intellij-formatter.xml 다운로드
- Schmem 설정
    - `File > Settings 메뉴로 이동한다. (단축키 Alt + Shift + S )`
    - `Editor > Code Style > Java 항목으로 이동한다.`
    - `Scheme 항목의 오른쪽에 있는 톱니바퀴 아이콘을 클릭한다.`
    - `Import Scheme > IntelliJ IDEA Code Style XML 을 선택한다.`
    - `1에서 다운로드한 naver-intellij-formatter.xml 파일을 선택한후 [OK] 버튼을 누른다.`
    - `TO 항목에는 naver-intellij-formatter.xml 안에 선언된 'Naver-Coding-Convnetion-v1.2’와 같은 이름이 디폴트로 나온다. 이 이름은 IntelliJ에서 전역적인 식별자가 되어서 다른 프로젝트에도 참조가 된다. 포멧터를 커스터 마이징했거나 프로젝트마다 다른 포멧터 설정을 쓴다면 이 스키마의 이름이 유일성 있게 인지되도록 수정한다.`
    
 - ***[캠퍼스 핵데이 Java 코딩 컨벤션](https://naver.github.io/hackday-conventions-java/#editorconfig)***