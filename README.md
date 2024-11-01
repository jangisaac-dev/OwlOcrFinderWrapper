# OwlOcrFinderWrapper
- owl ocr 앱 기능중, finder에서 바로 추출시 발생하는 문제를 해결하기 위해 automation파일로 제작
- 해당 기능 사용시, 같은 위치, 같은 파일명으로 *_ocr.pdf 파일과 *.txt 파일 생성
- 언어 선택 기능없음(자동)
- 한글 정상 작동 확인

apple script
```applescript
on run {input, parameters}
    repeat with f in input
        set filePath to POSIX path of f
        set baseFilePath to text 1 thru -5 of filePath -- 확장자 ".pdf" 제거
        set outputFilePath to baseFilePath & "_ocr.pdf"
        set resultFilePath to baseFilePath & ".txt"
        
        -- 명령어 실행 및 결과 저장 (출력 파일 및 텍스트 결과)
        do shell script "/Applications/OwlOCR.app/Contents/MacOS/OwlOCR --cli --input " & quoted form of filePath & " --output " & quoted form of outputFilePath & " | tee " & quoted form of resultFilePath
    end repeat
    return input
end run
```
