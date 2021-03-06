# A0155428B-unused
###### /resources/view/MainWindowLight.fxml
``` fxml
<fx:root type="javafx.stage.Stage" xmlns="http://javafx.com/javafx/8" xmlns:fx="http://javafx.com/fxml/1"
         minWidth="450" minHeight="600">
  <icons>
    <Image url="@/images/address_book_32.png" />
  </icons>
  <scene>
    <Scene>
      <stylesheets>
        <URL value="@LightTheme.css" />
        <URL value="@ExtensionsLight.css" />
      </stylesheets>

      <VBox>
        <MenuBar fx:id="menuBar" VBox.vgrow="NEVER">
          <Menu mnemonicParsing="false" text="File">
            <MenuItem mnemonicParsing="false" onAction="#handleExit" text="Exit" />
          </Menu>
          <Menu mnemonicParsing="false" text="Help">
            <MenuItem fx:id="helpMenuItem" mnemonicParsing="false" onAction="#handleHelp" text="Help" />
          </Menu>
        </MenuBar>

        <StackPane VBox.vgrow="NEVER" fx:id="commandBoxPlaceholder" styleClass="pane-with-border">
          <padding>
            <Insets top="5" right="10" bottom="5" left="10" />
          </padding>
        </StackPane>

        <StackPane VBox.vgrow="NEVER" fx:id="resultDisplayPlaceholder" styleClass="pane-with-border"
                   minHeight="100" prefHeight="100" maxHeight="100">
          <padding>
            <Insets top="5" right="10" bottom="5" left="10" />
          </padding>
        </StackPane>

        <SplitPane id="splitPane" fx:id="splitPane" dividerPositions="0.4" VBox.vgrow="ALWAYS">
          <VBox fx:id="personList" minWidth="340" prefWidth="340" SplitPane.resizableWithParent="false">
            <padding>
              <Insets top="10" right="10" bottom="10" left="10" />
            </padding>
            <StackPane fx:id="personListPanelPlaceholder" VBox.vgrow="ALWAYS"/>
          </VBox>

          <StackPane fx:id="browserPlaceholder" prefWidth="340" >
            <padding>
              <Insets top="10" right="10" bottom="10" left="10" />
            </padding>
          </StackPane>
        </SplitPane>

        <StackPane fx:id="statusbarPlaceholder" VBox.vgrow="NEVER" />
      </VBox>
    </Scene>
  </scene>
</fx:root>
```
###### /resources/view/ExtensionsLight.css
``` css
.error {
    -fx-text-fill: #d06651 !important; /* The error class should always override the default text-fill style */
}

.list-cell:empty {
    /* Empty cells will not have alternating colours */
    -fx-background: white;
}

.tag-selector {
    -fx-border-width: 1;
    -fx-border-color: white;
    -fx-border-radius: 3;
    -fx-background-radius: 3;
}

.tooltip-text {
    -fx-text-fill: white;
}
```
###### /java/seedu/address/model/UserPrefs.java
``` java
    public String getMainWindowFile() {
        return mainWindowFilePath;
    }

    public void setMainWindowFilePath(String newFilePath) {
        this.mainWindowFilePath = newFilePath;
    }

```
###### /java/seedu/address/model/ModelManager.java
``` java
    @Override
    public void updateTheme(String theme) throws InputThemeEqualsCurrentThemeException {
        if (theme.equals("light")) {
            if (this.userPrefs.getMainWindowFile().equals("MainWindowLight.fxml")) {
                throw new InputThemeEqualsCurrentThemeException();
            }
            this.userPrefs.setMainWindowFilePath("MainWindowLight.fxml");
        } else {
            if (this.userPrefs.getMainWindowFile().equals("MainWindow.fxml")) {
                throw new InputThemeEqualsCurrentThemeException();
            }
            this.userPrefs.setMainWindowFilePath("MainWindow.fxml");
        }
    }

    @Override
    public String getThemeFilePath() {
        return this.userPrefs.getGuiSettings().getThemeFilePath();
    }
}
```
###### /java/seedu/address/model/Exception/InputThemeEqualsCurrentThemeException.java
``` java
/**
 * Signals that the input theme is the current theme
 */
public class InputThemeEqualsCurrentThemeException extends Exception {
    public InputThemeEqualsCurrentThemeException() {
        super();
    }
}
```
