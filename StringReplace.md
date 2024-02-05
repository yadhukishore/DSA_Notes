# Replacing the Entered string with the enterd count

```javascript
//for UpperCase and lowerCase
function replaceString(inptStr,n){
    const isUpperCase = (char)=>char===char.toUpperCase();
    const replaceChar=(char)=>{
        let baseCharCode;
        if(isUpperCase(char)){
             baseCharCode = 'A'.charCodeAt(0);
        }else{
             baseCharCode = 'a'.charCodeAt(0);
        }
        const originalCharCode = char.charCodeAt(0);
        
        const newCharCode = baseCharCode+(originalCharCode-baseCharCode+n)%26;
        
        return String.fromCharCode(newCharCode);
    }
    const result = inptStr.replace(/[a-zA-Z]/g,(char)=>replaceChar(char));
    return result;
}

const str ="Hai,Yadhuu!";
const result = replaceString(str,1);
console.log(result);
//output = Ibj,Zbeivv!

```

## Replacing the lowerCase Strings only:-

```javascript
//for UpperCase and lowerCase
function replaceString(inptStr,n){
    const replaceChar=(char)=>{
        const baseCharCode = 'a'.charCodeAt(0);
        const originalCharCode = char.charCodeAt(0);
        
        const newCharCode = baseCharCode+(originalCharCode-baseCharCode+n)%26;
        
        return String.fromCharCode(newCharCode);
    }
    const result = inptStr.replace(/[a-z]/g,(char)=>replaceChar(char));
    return result;
}

const str ="d,yT";
const result = replaceString(str,1);
console.log(result);//e,zT

```
