---
title: Nazwa <namespacename> w głównej przestrzeni nazw <fullnamespacename> jest niezgodna ze specyfikacją CLS
ms.date: 07/20/2015
f1_keywords:
- vbc40039
- bc40039
helpviewer_keywords:
- BC40039
ms.assetid: c5bd5914-ae71-416a-8bed-f76f644f78be
ms.openlocfilehash: 48e020cb74641279a4f402e47034514d78dfc4fc
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2020
ms.locfileid: "92160213"
---
# <a name="bc40039-name-namespacename-in-the-root-namespace-fullnamespacename-is-not-cls-compliant"></a>BC40039: nazwa \<namespacename> w głównej przestrzeni nazw \<fullnamespacename> jest niezgodna ze specyfikacją CLS

Zestaw jest oznaczony jako `<CLSCompliant(True)>` , ale element nazwy głównej przestrzeni nazw zaczyna się od znaku podkreślenia ( `_` ).

 Element programowania może zawierać jeden lub więcej podkreśleń, ale w celu uzyskania zgodności z [niezależnymi od języka i składnikami Language-Independent](../../../standard/language-independence-and-language-independent-components.md) (CLS) nie może zaczynać się od znaku podkreślenia. Zobacz [zadeklarowane nazwy elementów](../../programming-guide/language-features/declared-elements/declared-element-names.md).

 Po zastosowaniu <xref:System.CLSCompliantAttribute> do elementu programistycznego, należy ustawić `isCompliant` parametr atrybutu na wartość `True` lub `False` w celu wskazania zgodności lub niezgodności. Dla tego parametru nie ma wartości domyślnej i należy podać wartość.

 Jeśli nie zastosujesz <xref:System.CLSCompliantAttribute> do elementu, jest on uznawany za niezgodny.

 Domyślnie ten komunikat jest ostrzeżeniem. Aby uzyskać informacje na temat ukrywania ostrzeżeń lub leczenia ostrzeżeń jako błędy, zobacz [Konfigurowanie ostrzeżeń w Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic).

 **Identyfikator błędu:** BC40039

## <a name="to-correct-this-error"></a>Aby poprawić ten błąd

- Jeśli jest wymagana zgodność ze specyfikacją CLS, Zmień nazwę głównej przestrzeni nazw, tak aby żaden z jej elementów nie zaczynał się od znaku podkreślenia.

- Jeśli potrzebujesz, aby nazwa przestrzeni nazw pozostała niezmieniona, Usuń <xref:System.CLSCompliantAttribute> z zestawu lub oznacz ją jako `<CLSCompliant(False)>` .

## <a name="see-also"></a>Zobacz też

- [Namespace — Instrukcja](../statements/namespace-statement.md)
- [Przestrzenie nazw w Visual Basic](../../programming-guide/program-structure/namespaces.md)
- [-rootnamespace](../../reference/command-line-compiler/rootnamespace.md)
- [Strona aplikacji, Projektant projektu (Visual Basic)](/visualstudio/ide/reference/application-page-project-designer-visual-basic)
- [Nazwy zadeklarowanych elementów](../../programming-guide/language-features/declared-elements/declared-element-names.md)
- [Visual Basic — Konwencje nazewnictwa](../../programming-guide/program-structure/naming-conventions.md)
