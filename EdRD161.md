## [D: Berserk Monster](https://codeforces.com/problemset/problem/1922/D)

<details>
  <summary>tags</summary>
  
    | brute force | data structure |

</details>

<details>
  <summary>solution</summary>

    The key is to notice that if A is not beaten this round, nor are its neighbours, then there's no way it dies in the next round.
    In other words, only death results in new candidates for death in the next round.

    At the beginning, all monsters are candidates.
    Every round check if the candidates die. If so, include their neighbours to the candidates of the next round.
    
</details>

<details>
  <summary>code</summary>

  ```c++
  int main () {
      int t;  cin >> t;
      while (t--) {
          int n;  cin >> n;
          vector<ll> atk(n + 2), dfs(n + 2);
          for (int i = 1; i <= n; i++) cin >> atk[i];
          for (int i = 1; i <= n; i++) cin >> dfs[i];
          dfs[0] = dfs[n + 1] = LLONG_MAX;
  
          set<int> alive, to_check;
          for (int i = 0; i <= n + 1; i++) {
              alive.insert(i);
              to_check.insert(i);
          }
  
          for (int rd = 1; rd <= n; rd++) {
              set<int> check_nxt, beaten;
              for (auto x: to_check) {
                  auto it = alive.find(x);
                  if (it == alive.end()) continue;
  
                  int pre = *prev(it);
                  int nxt = *next(it);
                  if (atk[pre] + atk[nxt] > dfs[x]) {
                      beaten.insert(x);
                      check_nxt.insert(pre);
                      check_nxt.insert(nxt);
                  }
              }
              cout << beaten.size() << ' ';
  
              to_check = check_nxt;
              for (int x: beaten) {
                  alive.erase(x);
              }
          }
          cout << '\n';
      }
  }
  ```

</details>

<br>
