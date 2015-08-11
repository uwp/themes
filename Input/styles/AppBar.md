Title: AppBar
---
# AppBar


Control template without visual states
```xaml
<ControlTemplate TargetType="AppBar">
   <Grid x:Name="LayoutRoot" Background="{TemplateBinding Background}">
      <Grid.Clip>
         <RectangleGeometry Rect="{Binding RelativeSource={RelativeSource TemplatedParent},
                                           Path=TemplateSettings.ClipRect}">
            <RectangleGeometry.Transform>
               <TranslateTransform x:Name="ClipGeometryTransform"
                                   Y="{Binding RelativeSource={RelativeSource TemplatedParent},
                                               Path=TemplateSettings.CompactVerticalDelta}"
                                   />
            </RectangleGeometry.Transform>
         </RectangleGeometry>
      </Grid.Clip>
      <Grid x:Name="ContentRoot"
            VerticalAlignment="Top"
            Margin="{TemplateBinding Padding}"
            Height="{TemplateBinding Height}"
            MinHeight="{ThemeResource AppBarThemeMinHeight}"
            Background="{TemplateBinding Background}"
            Opacity="{TemplateBinding Opacity}"
            />
         <Grid.ColumnDefinitions>
            <ColumnDefinition Width="*" />
            <ColumnDefinition Width="Auto" />
         </Grid.ColumnDefinitions>
         <Grid.RenderTransform>
            <TranslateTransform x:Name="ContentTransform" />
         </Grid.RenderTransform>
         <ContentControl x:Name="ContentControl"
                         Content="{TemplateBinding Content}"
                         ContentTemplate="{TemplateBinding ContentTemplate}"
                         ContentTransitions="{TemplateBinding ContentTransitions}"
                         Foreground="{TemplateBinding Foreground}"
                         HorizontalAlignment="{TemplateBinding HorizontalContentAlignment}"
                         VerticalAlignment="{TemplateBinding VerticalContentAlignment}"
                         HorizontalContentAlignment="{TemplateBinding HorizontalContentAlignment}"
                         VerticalContentAlignment="{TemplateBinding VerticalContentAlignment}"
                         IsTabStop="False"
                         />
         <Button x:Name="ExpandButton"
                 Foreground="{TemplateBinding Foreground}"
                 Style="{StaticResource EllipsisButton}"
                 Padding="16,23,16,0"
                 MinHeight="{ThemeResource AppBarThemeCompactHeight}"
                 VerticalAlignment="Top"
                 Grid.Column="1"
                 />
            <FontIcon x:Name="EllipsisIcon"
                      VerticalAlignment="Center"
                      FontFamily="{ThemeResource SymbolThemeFontFamily}"
                      FontSize="16"
                      Glyph=""
                      Height="{ThemeResource AppBarExpandButtonCircleDiameter}"
                      />
         </Button>
         <Rectangle x:Name="HighContrastBorder"
                    x:DeferLoadStrategy="Lazy"
                    Grid.ColumnSpan="2"
                    Visibility="Collapsed"
                    VerticalAlignment="Stretch"
                    Stroke="{ThemeResource SystemControlForegroundTransparentBrush}"
                    StrokeThickness="1"
                    />
      </Grid>
   </Grid>
</ControlTemplate>
```
 - Group: CommonStates
   - State: Normal
   - State: Disabled
 - Group: DisplayModeStates
   - State: CompactClosed
   - State: CompactOpenUp
   - State: CompactOpenDown
   - State: MinimalClosed
   - State: MinimalOpenUp
   - State: MinimalOpenDown
   - State: HiddenClosed
   - State: HiddenOpenUp
   - State: HiddenOpenDown

Default style
```xaml
<Style TargetType="AppBar">
   <Setter Property="Background" Value="{ThemeResource SystemControlBackgroundChromeMediumBrush}" />
   <Setter Property="Foreground" Value="{ThemeResource SystemControlForegroundBaseHighBrush}" />
   <Setter Property="IsTabStop" Value="False" />
   <Setter Property="VerticalAlignment" Value="Top" />
   <Setter Property="HorizontalAlignment" Value="Stretch" />
   <Setter Property="HorizontalContentAlignment" Value="Stretch" />
   <Setter Property="VerticalContentAlignment" Value="Stretch" />
   <Setter Property="ClosedDisplayMode" Value="Minimal" />
   <Setter Property="Template">
      <Setter.Value>
         <ControlTemplate TargetType="AppBar">
            <Grid x:Name="LayoutRoot" Background="{TemplateBinding Background}">
               <VisualStateManager.VisualStateGroups>
                  <VisualStateGroup x:Name="CommonStates">
                     <VisualState x:Name="Normal" />
                     <VisualState x:Name="Disabled">
                        <Storyboard>
                           <ObjectAnimationUsingKeyFrames Storyboard.TargetName="EllipsisIcon"
                                                          Storyboard.TargetProperty="Foreground"
                                                          />
                              <DiscreteObjectKeyFrame KeyTime="0"
                                                      Value="{ThemeResource SystemControlDisabledBaseLowBrush}"
                                                      />
                           </ObjectAnimationUsingKeyFrames>
                        </Storyboard>
                     </VisualState>
                  </VisualStateGroup>
                  <VisualStateGroup x:Name="DisplayModeStates">
                     <VisualStateGroup.Transitions>
                        <VisualTransition From="CompactClosed"
                                          To="CompactOpenUp"
                                          GeneratedDuration="0:0:0.667"
                                          />
                           <Storyboard>
                              <ObjectAnimationUsingKeyFrames Storyboard.TargetName="ExpandButton"
                                                             Storyboard.TargetProperty="VerticalAlignment"
                                                             />
                                 <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="Stretch" />
                              </ObjectAnimationUsingKeyFrames>
                              <ObjectAnimationUsingKeyFrames Storyboard.TargetName="HighContrastBorder"
                                                             Storyboard.TargetProperty="Visibility"
                                                             />
                                 <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="Visible" />
                              </ObjectAnimationUsingKeyFrames>
                              <DoubleAnimationUsingKeyFrames Storyboard.TargetName="ContentTransform"
                                                             Storyboard.TargetProperty="Y"
                                                             />
                                 <DiscreteDoubleKeyFrame KeyTime="0:0:0" Value="0" />
                                 <SplineDoubleKeyFrame KeyTime="0:0:0.667"
                                                       KeySpline="0.1,0.9 0.2,1.0"
                                                       Value="{Binding RelativeSource={RelativeSource TemplatedParent},
                                                                       Path=TemplateSettings.CompactVerticalDelta}"
                                                       />
                              </DoubleAnimationUsingKeyFrames>
                           </Storyboard>
                        </VisualTransition>
                        <VisualTransition From="CompactOpenUp"
                                          To="CompactClosed"
                                          GeneratedDuration="0:0:0.167"
                                          />
                           <Storyboard>
                              <ObjectAnimationUsingKeyFrames Storyboard.TargetName="ExpandButton"
                                                             Storyboard.TargetProperty="VerticalAlignment"
                                                             />
                                 <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="Stretch" />
                              </ObjectAnimationUsingKeyFrames>
                              <ObjectAnimationUsingKeyFrames Storyboard.TargetName="HighContrastBorder"
                                                             Storyboard.TargetProperty="Visibility"
                                                             />
                                 <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="Visible" />
                              </ObjectAnimationUsingKeyFrames>
                              <DoubleAnimationUsingKeyFrames Storyboard.TargetName="ContentTransform"
                                                             Storyboard.TargetProperty="Y"
                                                             />
                                 <DiscreteDoubleKeyFrame KeyTime="0:0:0"
                                                         Value="{Binding RelativeSource={RelativeSource TemplatedParent},
                                                                         Path=TemplateSettings.CompactVerticalDelta}"
                                                         />
                                 <SplineDoubleKeyFrame KeyTime="0:0:0.167"
                                                       KeySpline="0.9,0.1 0.2,1.0"
                                                       Value="0"
                                                       />
                              </DoubleAnimationUsingKeyFrames>
                           </Storyboard>
                        </VisualTransition>
                        <VisualTransition From="CompactClosed"
                                          To="CompactOpenDown"
                                          GeneratedDuration="0:0:0.667"
                                          />
                           <Storyboard>
                              <ObjectAnimationUsingKeyFrames Storyboard.TargetName="ExpandButton"
                                                             Storyboard.TargetProperty="VerticalAlignment"
                                                             />
                                 <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="Stretch" />
                              </ObjectAnimationUsingKeyFrames>
                              <ObjectAnimationUsingKeyFrames Storyboard.TargetName="HighContrastBorder"
                                                             Storyboard.TargetProperty="Visibility"
                                                             />
                                 <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="Visible" />
                              </ObjectAnimationUsingKeyFrames>
                              <DoubleAnimationUsingKeyFrames Storyboard.TargetName="ClipGeometryTransform"
                                                             Storyboard.TargetProperty="Y"
                                                             />
                                 <DiscreteDoubleKeyFrame KeyTime="0:0:0"
                                                         Value="{Binding RelativeSource={RelativeSource TemplatedParent},
                                                                         Path=TemplateSettings.CompactVerticalDelta}"
                                                         />
                                 <SplineDoubleKeyFrame KeyTime="0:0:0.667"
                                                       KeySpline="0.1,0.9 0.2,1.0"
                                                       Value="0"
                                                       />
                              </DoubleAnimationUsingKeyFrames>
                           </Storyboard>
                        </VisualTransition>
                        <VisualTransition From="CompactOpenDown"
                                          To="CompactClosed"
                                          GeneratedDuration="0:0:0.167"
                                          />
                           <Storyboard>
                              <ObjectAnimationUsingKeyFrames Storyboard.TargetName="ExpandButton"
                                                             Storyboard.TargetProperty="VerticalAlignment"
                                                             />
                                 <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="Stretch" />
                              </ObjectAnimationUsingKeyFrames>
                              <ObjectAnimationUsingKeyFrames Storyboard.TargetName="HighContrastBorder"
                                                             Storyboard.TargetProperty="Visibility"
                                                             />
                                 <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="Visible" />
                              </ObjectAnimationUsingKeyFrames>
                              <DoubleAnimationUsingKeyFrames Storyboard.TargetName="ClipGeometryTransform"
                                                             Storyboard.TargetProperty="Y"
                                                             />
                                 <DiscreteDoubleKeyFrame KeyTime="0:0:0" Value="0" />
                                 <SplineDoubleKeyFrame KeyTime="0:0:0.167"
                                                       KeySpline="0.9,0.1 0.2,1.0"
                                                       Value="{Binding RelativeSource={RelativeSource TemplatedParent},
                                                                       Path=TemplateSettings.CompactVerticalDelta}"
                                                       />
                              </DoubleAnimationUsingKeyFrames>
                           </Storyboard>
                        </VisualTransition>
                        <VisualTransition From="MinimalClosed"
                                          To="MinimalOpenUp"
                                          GeneratedDuration="0:0:0.667"
                                          />
                           <Storyboard>
                              <ObjectAnimationUsingKeyFrames Storyboard.TargetName="ExpandButton"
                                                             Storyboard.TargetProperty="Padding"
                                                             />
                                 <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="16,11,16,0" />
                              </ObjectAnimationUsingKeyFrames>
                              <ObjectAnimationUsingKeyFrames Storyboard.TargetName="ExpandButton"
                                                             Storyboard.TargetProperty="VerticalAlignment"
                                                             />
                                 <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="Stretch" />
                              </ObjectAnimationUsingKeyFrames>
                              <ObjectAnimationUsingKeyFrames Storyboard.TargetName="HighContrastBorder"
                                                             Storyboard.TargetProperty="Visibility"
                                                             />
                                 <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="Visible" />
                              </ObjectAnimationUsingKeyFrames>
                              <DoubleAnimationUsingKeyFrames Storyboard.TargetName="ClipGeometryTransform"
                                                             Storyboard.TargetProperty="Y"
                                                             />
                                 <DiscreteDoubleKeyFrame KeyTime="0:0:0"
                                                         Value="{Binding RelativeSource={RelativeSource TemplatedParent},
                                                                         Path=TemplateSettings.MinimalVerticalDelta}"
                                                         />
                              </DoubleAnimationUsingKeyFrames>
                              <DoubleAnimationUsingKeyFrames Storyboard.TargetName="ContentTransform"
                                                             Storyboard.TargetProperty="Y"
                                                             />
                                 <DiscreteDoubleKeyFrame KeyTime="0:0:0" Value="0" />
                                 <SplineDoubleKeyFrame KeyTime="0:0:0.667"
                                                       KeySpline="0.1,0.9 0.2,1.0"
                                                       Value="{Binding RelativeSource={RelativeSource TemplatedParent},
                                                                       Path=TemplateSettings.MinimalVerticalDelta}"
                                                       />
                              </DoubleAnimationUsingKeyFrames>
                              <DoubleAnimationUsingKeyFrames Storyboard.TargetName="ContentControl"
                                                             Storyboard.TargetProperty="Opacity"
                                                             />
                                 <DiscreteDoubleKeyFrame KeyTime="0:0:0" Value="0" />
                                 <SplineDoubleKeyFrame KeyTime="0:0:0.667"
                                                       KeySpline="0.1,0.9 0.2,1.0"
                                                       Value="1"
                                                       />
                              </DoubleAnimationUsingKeyFrames>
                           </Storyboard>
                        </VisualTransition>
                        <VisualTransition From="MinimalOpenUp"
                                          To="MinimalClosed"
                                          GeneratedDuration="0:0:0.167"
                                          />
                           <Storyboard>
                              <ObjectAnimationUsingKeyFrames Storyboard.TargetName="ExpandButton"
                                                             Storyboard.TargetProperty="Padding"
                                                             />
                                 <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="16,11,16,0" />
                              </ObjectAnimationUsingKeyFrames>
                              <ObjectAnimationUsingKeyFrames Storyboard.TargetName="ExpandButton"
                                                             Storyboard.TargetProperty="VerticalAlignment"
                                                             />
                                 <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="Stretch" />
                              </ObjectAnimationUsingKeyFrames>
                              <ObjectAnimationUsingKeyFrames Storyboard.TargetName="HighContrastBorder"
                                                             Storyboard.TargetProperty="Visibility"
                                                             />
                                 <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="Visible" />
                              </ObjectAnimationUsingKeyFrames>
                              <DoubleAnimationUsingKeyFrames Storyboard.TargetName="ClipGeometryTransform"
                                                             Storyboard.TargetProperty="Y"
                                                             />
                                 <DiscreteDoubleKeyFrame KeyTime="0:0:0"
                                                         Value="{Binding RelativeSource={RelativeSource TemplatedParent},
                                                                         Path=TemplateSettings.MinimalVerticalDelta}"
                                                         />
                              </DoubleAnimationUsingKeyFrames>
                              <DoubleAnimationUsingKeyFrames Storyboard.TargetName="ContentTransform"
                                                             Storyboard.TargetProperty="Y"
                                                             />
                                 <DiscreteDoubleKeyFrame KeyTime="0:0:0"
                                                         Value="{Binding RelativeSource={RelativeSource TemplatedParent},
                                                                         Path=TemplateSettings.MinimalVerticalDelta}"
                                                         />
                                 <SplineDoubleKeyFrame KeyTime="0:0:0.167"
                                                       KeySpline="0.9,0.1 0.2,1.0"
                                                       Value="0"
                                                       />
                              </DoubleAnimationUsingKeyFrames>
                              <DoubleAnimationUsingKeyFrames Storyboard.TargetName="ContentControl"
                                                             Storyboard.TargetProperty="Opacity"
                                                             />
                                 <DiscreteDoubleKeyFrame KeyTime="0:0:0" Value="1" />
                                 <SplineDoubleKeyFrame KeyTime="0:0:0.167"
                                                       KeySpline="0.9,0.1 0.2,1.0"
                                                       Value="0"
                                                       />
                              </DoubleAnimationUsingKeyFrames>
                           </Storyboard>
                        </VisualTransition>
                        <VisualTransition From="MinimalClosed"
                                          To="MinimalOpenDown"
                                          GeneratedDuration="0:0:0.667"
                                          />
                           <Storyboard>
                              <ObjectAnimationUsingKeyFrames Storyboard.TargetName="ExpandButton"
                                                             Storyboard.TargetProperty="Padding"
                                                             />
                                 <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="16,11,16,0" />
                              </ObjectAnimationUsingKeyFrames>
                              <ObjectAnimationUsingKeyFrames Storyboard.TargetName="ExpandButton"
                                                             Storyboard.TargetProperty="VerticalAlignment"
                                                             />
                                 <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="Stretch" />
                              </ObjectAnimationUsingKeyFrames>
                              <ObjectAnimationUsingKeyFrames Storyboard.TargetName="HighContrastBorder"
                                                             Storyboard.TargetProperty="Visibility"
                                                             />
                                 <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="Visible" />
                              </ObjectAnimationUsingKeyFrames>
                              <DoubleAnimationUsingKeyFrames Storyboard.TargetName="ClipGeometryTransform"
                                                             Storyboard.TargetProperty="Y"
                                                             />
                                 <DiscreteDoubleKeyFrame KeyTime="0:0:0"
                                                         Value="{Binding RelativeSource={RelativeSource TemplatedParent},
                                                                         Path=TemplateSettings.MinimalVerticalDelta}"
                                                         />
                                 <SplineDoubleKeyFrame KeyTime="0:0:0.667"
                                                       KeySpline="0.1,0.9 0.2,1.0"
                                                       Value="0"
                                                       />
                              </DoubleAnimationUsingKeyFrames>
                              <DoubleAnimationUsingKeyFrames Storyboard.TargetName="ContentControl"
                                                             Storyboard.TargetProperty="Opacity"
                                                             />
                                 <DiscreteDoubleKeyFrame KeyTime="0:0:0" Value="0" />
                                 <SplineDoubleKeyFrame KeyTime="0:0:0.667"
                                                       KeySpline="0.1,0.9 0.2,1.0"
                                                       Value="1"
                                                       />
                              </DoubleAnimationUsingKeyFrames>
                           </Storyboard>
                        </VisualTransition>
                        <VisualTransition From="MinimalOpenDown"
                                          To="MinimalClosed"
                                          GeneratedDuration="0:0:0.167"
                                          />
                           <Storyboard>
                              <ObjectAnimationUsingKeyFrames Storyboard.TargetName="ExpandButton"
                                                             Storyboard.TargetProperty="Padding"
                                                             />
                                 <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="16,11,16,0" />
                              </ObjectAnimationUsingKeyFrames>
                              <ObjectAnimationUsingKeyFrames Storyboard.TargetName="ExpandButton"
                                                             Storyboard.TargetProperty="VerticalAlignment"
                                                             />
                                 <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="Stretch" />
                              </ObjectAnimationUsingKeyFrames>
                              <ObjectAnimationUsingKeyFrames Storyboard.TargetName="HighContrastBorder"
                                                             Storyboard.TargetProperty="Visibility"
                                                             />
                                 <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="Visible" />
                              </ObjectAnimationUsingKeyFrames>
                              <DoubleAnimationUsingKeyFrames Storyboard.TargetName="ClipGeometryTransform"
                                                             Storyboard.TargetProperty="Y"
                                                             />
                                 <DiscreteDoubleKeyFrame KeyTime="0:0:0" Value="0" />
                                 <SplineDoubleKeyFrame KeyTime="0:0:0.167"
                                                       KeySpline="0.9,0.1 0.2,1.0"
                                                       Value="{Binding RelativeSource={RelativeSource TemplatedParent},
                                                                       Path=TemplateSettings.MinimalVerticalDelta}"
                                                       />
                              </DoubleAnimationUsingKeyFrames>
                              <DoubleAnimationUsingKeyFrames Storyboard.TargetName="ContentControl"
                                                             Storyboard.TargetProperty="Opacity"
                                                             />
                                 <DiscreteDoubleKeyFrame KeyTime="0:0:0" Value="1" />
                                 <SplineDoubleKeyFrame KeyTime="0:0:0.167"
                                                       KeySpline="0.9,0.1 0.2,1.0"
                                                       Value="0"
                                                       />
                              </DoubleAnimationUsingKeyFrames>
                           </Storyboard>
                        </VisualTransition>
                        <VisualTransition From="HiddenClosed"
                                          To="HiddenOpenUp"
                                          GeneratedDuration="0:0:0.667"
                                          />
                           <Storyboard>
                              <ObjectAnimationUsingKeyFrames Storyboard.TargetName="ExpandButton"
                                                             Storyboard.TargetProperty="VerticalAlignment"
                                                             />
                                 <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="Stretch" />
                              </ObjectAnimationUsingKeyFrames>
                              <ObjectAnimationUsingKeyFrames Storyboard.TargetName="HighContrastBorder"
                                                             Storyboard.TargetProperty="Visibility"
                                                             />
                                 <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="Visible" />
                              </ObjectAnimationUsingKeyFrames>
                              <DoubleAnimationUsingKeyFrames Storyboard.TargetName="ContentTransform"
                                                             Storyboard.TargetProperty="Y"
                                                             />
                                 <DiscreteDoubleKeyFrame KeyTime="0:0:0" Value="0" />
                                 <SplineDoubleKeyFrame KeyTime="0:0:0.667"
                                                       KeySpline="0.1,0.9 0.2,1.0"
                                                       Value="{Binding RelativeSource={RelativeSource TemplatedParent},
                                                                       Path=TemplateSettings.HiddenVerticalDelta}"
                                                       />
                              </DoubleAnimationUsingKeyFrames>
                           </Storyboard>
                        </VisualTransition>
                        <VisualTransition From="HiddenOpenUp"
                                          To="HiddenClosed"
                                          GeneratedDuration="0:0:0.167"
                                          />
                           <Storyboard>
                              <ObjectAnimationUsingKeyFrames Storyboard.TargetName="ExpandButton"
                                                             Storyboard.TargetProperty="VerticalAlignment"
                                                             />
                                 <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="Stretch" />
                              </ObjectAnimationUsingKeyFrames>
                              <ObjectAnimationUsingKeyFrames Storyboard.TargetName="HighContrastBorder"
                                                             Storyboard.TargetProperty="Visibility"
                                                             />
                                 <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="Visible" />
                              </ObjectAnimationUsingKeyFrames>
                              <DoubleAnimationUsingKeyFrames Storyboard.TargetName="ContentTransform"
                                                             Storyboard.TargetProperty="Y"
                                                             />
                                 <DiscreteDoubleKeyFrame KeyTime="0:0:0"
                                                         Value="{Binding RelativeSource={RelativeSource TemplatedParent},
                                                                         Path=TemplateSettings.HiddenVerticalDelta}"
                                                         />
                                 <SplineDoubleKeyFrame KeyTime="0:0:0.167"
                                                       KeySpline="0.1,0.9 0.2,1.0"
                                                       Value="0}"
                                                       />
                              </DoubleAnimationUsingKeyFrames>
                           </Storyboard>
                        </VisualTransition>
                        <VisualTransition From="HiddenClosed"
                                          To="HiddenOpenDown"
                                          GeneratedDuration="0:0:0.667"
                                          />
                           <Storyboard>
                              <ObjectAnimationUsingKeyFrames Storyboard.TargetName="ExpandButton"
                                                             Storyboard.TargetProperty="VerticalAlignment"
                                                             />
                                 <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="Stretch" />
                              </ObjectAnimationUsingKeyFrames>
                              <ObjectAnimationUsingKeyFrames Storyboard.TargetName="HighContrastBorder"
                                                             Storyboard.TargetProperty="Visibility"
                                                             />
                                 <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="Visible" />
                              </ObjectAnimationUsingKeyFrames>
                              <DoubleAnimationUsingKeyFrames Storyboard.TargetName="ClipGeometryTransform"
                                                             Storyboard.TargetProperty="Y"
                                                             />
                                 <DiscreteDoubleKeyFrame KeyTime="0:0:0"
                                                         Value="{Binding RelativeSource={RelativeSource TemplatedParent},
                                                                         Path=TemplateSettings.HiddenVerticalDelta}"
                                                         />
                                 <SplineDoubleKeyFrame KeyTime="0:0:0.667"
                                                       KeySpline="0.1,0.9 0.2,1.0"
                                                       Value="0"
                                                       />
                              </DoubleAnimationUsingKeyFrames>
                           </Storyboard>
                        </VisualTransition>
                        <VisualTransition From="HiddenOpenDown"
                                          To="HiddenClosed"
                                          GeneratedDuration="0:0:0.167"
                                          />
                           <Storyboard>
                              <ObjectAnimationUsingKeyFrames Storyboard.TargetName="ExpandButton"
                                                             Storyboard.TargetProperty="VerticalAlignment"
                                                             />
                                 <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="Stretch" />
                              </ObjectAnimationUsingKeyFrames>
                              <ObjectAnimationUsingKeyFrames Storyboard.TargetName="HighContrastBorder"
                                                             Storyboard.TargetProperty="Visibility"
                                                             />
                                 <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="Visible" />
                              </ObjectAnimationUsingKeyFrames>
                              <DoubleAnimationUsingKeyFrames Storyboard.TargetName="ClipGeometryTransform"
                                                             Storyboard.TargetProperty="Y"
                                                             />
                                 <DiscreteDoubleKeyFrame KeyTime="0:0:0" Value="0" />
                                 <SplineDoubleKeyFrame KeyTime="0:0:0.167"
                                                       KeySpline="0.9,0.1 0.2,1.0"
                                                       Value="{Binding RelativeSource={RelativeSource TemplatedParent},
                                                                       Path=TemplateSettings.HiddenVerticalDelta}"
                                                       />
                              </DoubleAnimationUsingKeyFrames>
                           </Storyboard>
                        </VisualTransition>
                     </VisualStateGroup.Transitions>
                     <VisualState x:Name="CompactClosed" />
                     <VisualState x:Name="CompactOpenUp">
                        <Storyboard>
                           <DoubleAnimationUsingKeyFrames Storyboard.TargetName="ContentTransform"
                                                          Storyboard.TargetProperty="Y"
                                                          />
                              <DiscreteDoubleKeyFrame KeyTime="0:0:0"
                                                      Value="{Binding RelativeSource={RelativeSource TemplatedParent},
                                                                      Path=TemplateSettings.CompactVerticalDelta}"
                                                      />
                           </DoubleAnimationUsingKeyFrames>
                           <ObjectAnimationUsingKeyFrames Storyboard.TargetName="ExpandButton"
                                                          Storyboard.TargetProperty="VerticalAlignment"
                                                          />
                              <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="Stretch" />
                           </ObjectAnimationUsingKeyFrames>
                           <ObjectAnimationUsingKeyFrames Storyboard.TargetName="HighContrastBorder"
                                                          Storyboard.TargetProperty="Visibility"
                                                          />
                              <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="Visible" />
                           </ObjectAnimationUsingKeyFrames>
                        </Storyboard>
                     </VisualState>
                     <VisualState x:Name="CompactOpenDown">
                        <Storyboard>
                           <DoubleAnimationUsingKeyFrames Storyboard.TargetName="ClipGeometryTransform"
                                                          Storyboard.TargetProperty="Y"
                                                          />
                              <DiscreteDoubleKeyFrame KeyTime="0:0:0" Value="0" />
                           </DoubleAnimationUsingKeyFrames>
                           <ObjectAnimationUsingKeyFrames Storyboard.TargetName="ExpandButton"
                                                          Storyboard.TargetProperty="VerticalAlignment"
                                                          />
                              <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="Stretch" />
                           </ObjectAnimationUsingKeyFrames>
                           <ObjectAnimationUsingKeyFrames Storyboard.TargetName="HighContrastBorder"
                                                          Storyboard.TargetProperty="Visibility"
                                                          />
                              <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="Visible" />
                           </ObjectAnimationUsingKeyFrames>
                        </Storyboard>
                     </VisualState>
                     <VisualState x:Name="MinimalClosed">
                        <Storyboard>
                           <DoubleAnimationUsingKeyFrames Storyboard.TargetName="ClipGeometryTransform"
                                                          Storyboard.TargetProperty="Y"
                                                          />
                              <DiscreteDoubleKeyFrame KeyTime="0:0:0"
                                                      Value="{Binding RelativeSource={RelativeSource TemplatedParent},
                                                                      Path=TemplateSettings.MinimalVerticalDelta}"
                                                      />
                           </DoubleAnimationUsingKeyFrames>
                           <ObjectAnimationUsingKeyFrames Storyboard.TargetName="ContentControl"
                                                          Storyboard.TargetProperty="IsHitTestVisible"
                                                          />
                              <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="False" />
                           </ObjectAnimationUsingKeyFrames>
                           <ObjectAnimationUsingKeyFrames Storyboard.TargetName="ContentControl"
                                                          Storyboard.TargetProperty="IsEnabled"
                                                          />
                              <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="False" />
                           </ObjectAnimationUsingKeyFrames>
                           <DoubleAnimationUsingKeyFrames Storyboard.TargetName="ContentControl"
                                                          Storyboard.TargetProperty="Opacity"
                                                          />
                              <DiscreteDoubleKeyFrame KeyTime="0:0:0" Value="0" />
                           </DoubleAnimationUsingKeyFrames>
                           <ObjectAnimationUsingKeyFrames Storyboard.TargetName="ExpandButton"
                                                          Storyboard.TargetProperty="MinHeight"
                                                          />
                              <DiscreteObjectKeyFrame KeyTime="0:0:0"
                                                      Value="{ThemeResource AppBarThemeMinimalHeight}"
                                                      />
                           </ObjectAnimationUsingKeyFrames>
                           <ObjectAnimationUsingKeyFrames Storyboard.TargetName="ExpandButton"
                                                          Storyboard.TargetProperty="Padding"
                                                          />
                              <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="16,11,16,0" />
                           </ObjectAnimationUsingKeyFrames>
                        </Storyboard>
                     </VisualState>
                     <VisualState x:Name="MinimalOpenUp">
                        <Storyboard>
                           <DoubleAnimationUsingKeyFrames Storyboard.TargetName="ClipGeometryTransform"
                                                          Storyboard.TargetProperty="Y"
                                                          />
                              <DiscreteDoubleKeyFrame KeyTime="0:0:0"
                                                      Value="{Binding RelativeSource={RelativeSource TemplatedParent},
                                                                      Path=TemplateSettings.MinimalVerticalDelta}"
                                                      />
                           </DoubleAnimationUsingKeyFrames>
                           <DoubleAnimationUsingKeyFrames Storyboard.TargetName="ContentTransform"
                                                          Storyboard.TargetProperty="Y"
                                                          />
                              <DiscreteDoubleKeyFrame KeyTime="0:0:0"
                                                      Value="{Binding RelativeSource={RelativeSource TemplatedParent},
                                                                      Path=TemplateSettings.MinimalVerticalDelta}"
                                                      />
                           </DoubleAnimationUsingKeyFrames>
                           <ObjectAnimationUsingKeyFrames Storyboard.TargetName="ExpandButton"
                                                          Storyboard.TargetProperty="Padding"
                                                          />
                              <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="16,11,16,0" />
                           </ObjectAnimationUsingKeyFrames>
                           <ObjectAnimationUsingKeyFrames Storyboard.TargetName="ExpandButton"
                                                          Storyboard.TargetProperty="VerticalAlignment"
                                                          />
                              <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="Stretch" />
                           </ObjectAnimationUsingKeyFrames>
                           <ObjectAnimationUsingKeyFrames Storyboard.TargetName="HighContrastBorder"
                                                          Storyboard.TargetProperty="Visibility"
                                                          />
                              <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="Visible" />
                           </ObjectAnimationUsingKeyFrames>
                        </Storyboard>
                     </VisualState>
                     <VisualState x:Name="MinimalOpenDown">
                        <Storyboard>
                           <DoubleAnimationUsingKeyFrames Storyboard.TargetName="ClipGeometryTransform"
                                                          Storyboard.TargetProperty="Y"
                                                          />
                              <DiscreteDoubleKeyFrame KeyTime="0:0:0" Value="0" />
                           </DoubleAnimationUsingKeyFrames>
                           <ObjectAnimationUsingKeyFrames Storyboard.TargetName="ExpandButton"
                                                          Storyboard.TargetProperty="Padding"
                                                          />
                              <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="16,11,16,0" />
                           </ObjectAnimationUsingKeyFrames>
                           <ObjectAnimationUsingKeyFrames Storyboard.TargetName="ExpandButton"
                                                          Storyboard.TargetProperty="VerticalAlignment"
                                                          />
                              <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="Stretch" />
                           </ObjectAnimationUsingKeyFrames>
                           <ObjectAnimationUsingKeyFrames Storyboard.TargetName="HighContrastBorder"
                                                          Storyboard.TargetProperty="Visibility"
                                                          />
                              <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="Visible" />
                           </ObjectAnimationUsingKeyFrames>
                        </Storyboard>
                     </VisualState>
                     <VisualState x:Name="HiddenClosed">
                        <Storyboard>
                           <DoubleAnimationUsingKeyFrames Storyboard.TargetName="ClipGeometryTransform"
                                                          Storyboard.TargetProperty="Y"
                                                          />
                              <DiscreteDoubleKeyFrame KeyTime="0:0:0"
                                                      Value="{Binding RelativeSource={RelativeSource TemplatedParent},
                                                                      Path=TemplateSettings.HiddenVerticalDelta}"
                                                      />
                           </DoubleAnimationUsingKeyFrames>
                           <ObjectAnimationUsingKeyFrames Storyboard.TargetName="ExpandButton"
                                                          Storyboard.TargetProperty="IsTabStop"
                                                          />
                              <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="False" />
                           </ObjectAnimationUsingKeyFrames>
                           <ObjectAnimationUsingKeyFrames Storyboard.TargetName="ContentControl"
                                                          Storyboard.TargetProperty="IsEnabled"
                                                          />
                              <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="False" />
                           </ObjectAnimationUsingKeyFrames>
                        </Storyboard>
                     </VisualState>
                     <VisualState x:Name="HiddenOpenUp">
                        <Storyboard>
                           <DoubleAnimationUsingKeyFrames Storyboard.TargetName="ClipGeometryTransform"
                                                          Storyboard.TargetProperty="Y"
                                                          />
                              <DiscreteDoubleKeyFrame KeyTime="0:0:0"
                                                      Value="{Binding RelativeSource={RelativeSource TemplatedParent},
                                                                      Path=TemplateSettings.HiddenVerticalDelta}"
                                                      />
                           </DoubleAnimationUsingKeyFrames>
                           <DoubleAnimationUsingKeyFrames Storyboard.TargetName="ContentTransform"
                                                          Storyboard.TargetProperty="Y"
                                                          />
                              <DiscreteDoubleKeyFrame KeyTime="0:0:0"
                                                      Value="{Binding RelativeSource={RelativeSource TemplatedParent},
                                                                      Path=TemplateSettings.HiddenVerticalDelta}"
                                                      />
                           </DoubleAnimationUsingKeyFrames>
                           <ObjectAnimationUsingKeyFrames Storyboard.TargetName="ExpandButton"
                                                          Storyboard.TargetProperty="VerticalAlignment"
                                                          />
                              <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="Stretch" />
                           </ObjectAnimationUsingKeyFrames>
                           <ObjectAnimationUsingKeyFrames Storyboard.TargetName="HighContrastBorder"
                                                          Storyboard.TargetProperty="Visibility"
                                                          />
                              <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="Visible" />
                           </ObjectAnimationUsingKeyFrames>
                        </Storyboard>
                     </VisualState>
                     <VisualState x:Name="HiddenOpenDown">
                        <Storyboard>
                           <DoubleAnimationUsingKeyFrames Storyboard.TargetName="ClipGeometryTransform"
                                                          Storyboard.TargetProperty="Y"
                                                          />
                              <DiscreteDoubleKeyFrame KeyTime="0:0:0" Value="0" />
                           </DoubleAnimationUsingKeyFrames>
                           <ObjectAnimationUsingKeyFrames Storyboard.TargetName="ExpandButton"
                                                          Storyboard.TargetProperty="VerticalAlignment"
                                                          />
                              <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="Stretch" />
                           </ObjectAnimationUsingKeyFrames>
                           <ObjectAnimationUsingKeyFrames Storyboard.TargetName="HighContrastBorder"
                                                          Storyboard.TargetProperty="Visibility"
                                                          />
                              <DiscreteObjectKeyFrame KeyTime="0:0:0" Value="Visible" />
                           </ObjectAnimationUsingKeyFrames>
                        </Storyboard>
                     </VisualState>
                  </VisualStateGroup>
               </VisualStateManager.VisualStateGroups>
               <Grid.Clip>
                  <RectangleGeometry Rect="{Binding RelativeSource={RelativeSource TemplatedParent},
                                                    Path=TemplateSettings.ClipRect}">
                     <RectangleGeometry.Transform>
                        <TranslateTransform x:Name="ClipGeometryTransform"
                                            Y="{Binding RelativeSource={RelativeSource TemplatedParent},
                                                        Path=TemplateSettings.CompactVerticalDelta}"
                                            />
                     </RectangleGeometry.Transform>
                  </RectangleGeometry>
               </Grid.Clip>
               <Grid x:Name="ContentRoot"
                     VerticalAlignment="Top"
                     Margin="{TemplateBinding Padding}"
                     Height="{TemplateBinding Height}"
                     MinHeight="{ThemeResource AppBarThemeMinHeight}"
                     Background="{TemplateBinding Background}"
                     Opacity="{TemplateBinding Opacity}"
                     />
                  <Grid.ColumnDefinitions>
                     <ColumnDefinition Width="*" />
                     <ColumnDefinition Width="Auto" />
                  </Grid.ColumnDefinitions>
                  <Grid.RenderTransform>
                     <TranslateTransform x:Name="ContentTransform" />
                  </Grid.RenderTransform>
                  <ContentControl x:Name="ContentControl"
                                  Content="{TemplateBinding Content}"
                                  ContentTemplate="{TemplateBinding ContentTemplate}"
                                  ContentTransitions="{TemplateBinding ContentTransitions}"
                                  Foreground="{TemplateBinding Foreground}"
                                  HorizontalAlignment="{TemplateBinding HorizontalContentAlignment}"
                                  VerticalAlignment="{TemplateBinding VerticalContentAlignment}"
                                  HorizontalContentAlignment="{TemplateBinding HorizontalContentAlignment}"
                                  VerticalContentAlignment="{TemplateBinding VerticalContentAlignment}"
                                  IsTabStop="False"
                                  />
                  <Button x:Name="ExpandButton"
                          Foreground="{TemplateBinding Foreground}"
                          Style="{StaticResource EllipsisButton}"
                          Padding="16,23,16,0"
                          MinHeight="{ThemeResource AppBarThemeCompactHeight}"
                          VerticalAlignment="Top"
                          Grid.Column="1"
                          />
                     <FontIcon x:Name="EllipsisIcon"
                               VerticalAlignment="Center"
                               FontFamily="{ThemeResource SymbolThemeFontFamily}"
                               FontSize="16"
                               Glyph=""
                               Height="{ThemeResource AppBarExpandButtonCircleDiameter}"
                               />
                  </Button>
                  <Rectangle x:Name="HighContrastBorder"
                             x:DeferLoadStrategy="Lazy"
                             Grid.ColumnSpan="2"
                             Visibility="Collapsed"
                             VerticalAlignment="Stretch"
                             Stroke="{ThemeResource SystemControlForegroundTransparentBrush}"
                             StrokeThickness="1"
                             />
               </Grid>
            </Grid>
         </ControlTemplate>
      </Setter.Value>
   </Setter>
</Style>
```
