# Bloquear capturas de ecrã (app Android com Capacitor)

Uma PWA não consegue bloquear capturas. Empacotada como app Android, sim (FLAG_SECURE).

```
npm init -y
npm i @capacitor/core @capacitor/cli @capacitor/android
npx cap init "Meus Gastos" com.pedromavakala.gastos --web-dir www
mkdir www && cp index.html manifest.json sw.js icon-*.png www/
npx cap add android
npx cap sync
```

Abre `android/app/src/main/java/com/pedromavakala/gastos/MainActivity.java` e deixa assim:

```java
package com.pedromavakala.gastos;

import android.os.Bundle;
import android.view.WindowManager;
import com.getcapacitor.BridgeActivity;

public class MainActivity extends BridgeActivity {
    @Override
    public void onCreate(Bundle savedInstanceState) {
        getWindow().setFlags(WindowManager.LayoutParams.FLAG_SECURE,
                             WindowManager.LayoutParams.FLAG_SECURE);
        super.onCreate(savedInstanceState);
    }
}
```

Depois: `npx cap open android` e, no Android Studio, Build > Build APK.
Os dados da app instalada são separados dos do navegador: usa "Gerar backup" no navegador e "Restaurar" na app.
