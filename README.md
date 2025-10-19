## 3.2 - Razor i dynamiczna data/rok
- **Adres:** `http://localhost:5000/`
- **Result:** pod „Welcome” jest **długa data**, a w stopce zawsze **bieżący rok**.
- **Done:** Użyłem Razor (`@DateTime.Now.ToString("D")`, `@DateTime.Now.Year`) do wstawiania aktualnej daty i roku.

## 3.3 - ViewData + warunek
- **Adres:** `http://localhost:5000/` (odśwież kilka razy)
- **Result:** wyświetla się **losowa liczba**; gdy `> 0,5`, ma **czerwone tło**.
- **Done:** Przekazałem `ViewData["random"]`, rzutowałem w widoku i użyłem `@if` do warunkowego formatowania.

## 3.4 - Silnie typowany model + scaffold listy
- **Adres:** `http://localhost:5000/Home/Index2`
- **Result:** **tabela** z kolumnami nazwanymi wg `DisplayName` (Imię, Nazwisko, itd.).
- **Done:** Widok `Index2` to scaffold „List” dla `Contact` – **strongly-typed** (`@model IEnumerable<Contact>`).

## 3.5 - Repozytorium (serwis) + DI
- **Adres:** `http://localhost:5000/Home/Index2`
- **Result:** wstępne rekordy (np. „Jan Kowalski”) pochodzą z **`PhoneBookService`**.
- **Done:** Dane trzymam w prostym serwisie i rejestruję go w DI (`AddSingleton`).

## 3.6 - Wstrzyknięcie serwisu do kontrolera
- **Adres:** `http://localhost:5000/Home/Index2`
- **Result:** lista pochodzi z **serwisu wstrzykniętego** do `HomeController` przez konstruktor.
- **Done:** Dependency Injection przekazuje serwis do kontrolera, a ten do widoku.

## 3.7 - Create (dodawanie)
- **Adres:** `http://localhost:5000/Home/Create`
- **Result:** wypełnij formularz (bez Id), **Zapisz** → pojawia się **nowy rekord** na `Index2`.
- **Done:** Widok `Create` tworzy `Contact`, a serwis nadaje `Id` i dodaje rekord.

## 3.8 - Delete (usuwanie)
- **Adres:** `http://localhost:5000/Home/Index2`
- **Result:** kliknij **Delete** przy wierszu - rekord **znika**, wracasz na listę.
- **Done:** `Delete(int id)` wywołuje `PhoneBookService.Remove(id)` i przekierowuje na `Index2`.

## 3.9 - Obsługa błędu (404 dla nieistniejącego Id)
- **Adres (GUI):** `http://localhost:5000/Home/Delete/9999` → **404**.  
- **Albo CLI:**
  ```bash
  curl -i http://localhost:5000/Home/Delete/9999
  ```
  (powinno zwrócić `HTTP/1.1 404 Not Found`)
- **Done:** Gdy `id` nie istnieje, kontroler zwraca `NotFound()` zamiast usuwać.