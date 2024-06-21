+ 공통된 스타일의 버튼이 존재할 경우 따로 button 스타일 파일을 만들어서 이용한다.

```swift
struct LoginBtnStyle: ButtonStyle {
    let textColor: Color
    let borderColor: Color
    
    init(
        textColor: Color,
        borderColor: Color? = nil
    ) {
        self.textColor = textColor
        self.borderColor = borderColor ?? textColor //nil 일 경우 textColor
    }
    
    func makeBody(configuration: Configuration) -> some View {
        configuration.label
            .font(.system(size: 14))
            .foregroundColor(self.textColor)
            .frame(maxWidth: .infinity, maxHeight: 40)
            .overlay {
                RoundedRectangle(cornerRadius: 5)
                    .stroke(self.borderColor, lineWidth: 0.8)
            }
            .padding(.horizontal,15)
            .opacity(configuration.isPressed ? 0.5 : 1) // configuration.isPressed 눌렀을 경우 0.5 : 1
    }
}

사용법 
        Button{
                // TODO: Apple
            }label: {
                Text("Apple 로그인")
            }
            .buttonStyle(LoginBtnStyle(textColor: .customBkText, borderColor: .customGreyLight))
```
