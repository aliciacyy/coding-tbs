---
label: Angular
---

### ngTemplate, ngTemplateOutlet and ngTemplateOutletContext

```Sample code
<ng-container *ngFor="let l of currentLetters" 
  [ngTemplateOutlet]="letterKey"
  [ngTemplateOutletContext]="{ letter: l }">
</ng-container>

<ng-template #letterKey let-letter="letter">
  <div class="letter-key" (click)="onLetterClick(letter)">{{letter}}</div>
</ng-template>
```