# final-averages
'Program Name: Final Averages Application
'Developer: Chris Gorman
'Date: 6/3/24
'Purpose: To input a name and ten grades then find the average and display all of them then write them to a text file

Public Class frmFinal
    'Declare class variables
    Private intSizeofArray As Integer = 9
    Private intGrades(intSizeofArray) As Integer
    Private strGrades(intSizeofArray) As String
    Private intCount As Integer = 0
    Private strStudentName As String
    Private intInputEntry As Integer = 1
    Private Sub btnNameAndGrades_Click(sender As Object, e As EventArgs) Handles btnNameAndGrades.Click
        'Variables
        Dim strNameInputMessage As String = "Enter students name"
        Dim strNameInputHeading As String = "Student Name"
        Dim blnGrade As Boolean = False
        Dim intTotalOfGrades As Integer
        Dim intAverage As Integer
        Dim objWriter As New IO.StreamWriter("F:\Visual Basic\Visual Basic Resources\Chapter 8\grades.txt")
        Dim strLocationandFileName As String = "F:\Visual Basic\Visual Basic Resources\Chapter 8\grades.txt"
        'Get the student name and display it in the program and the text file
        lstGrades.Items.Clear()
        intInputEntry = 1
        lblName.Visible = False
        lblAverage.Visible = False
        strStudentName = InputBox(strNameInputMessage, strNameInputHeading, "")
        If lblName.Text <> "" Then
            lblName.Visible = True
            lblName.Text = strStudentName
            If IO.File.Exists(strLocationandFileName) Then
                objWriter.WriteLine(strStudentName)
            End If
        End If
        'If the number was valid this adds one to the count and input entry then it adds the grade to the listbox
        For intCount = 0 To intSizeofArray
            If fncValidateGrade() Then
                intInputEntry += 1
                lstGrades.Items.Add(intGrades(intCount))
                intTotalOfGrades += intGrades(intCount)
            End If
        Next
        'Displays the average
        intAverage = Convert.ToInt32(intTotalOfGrades / (intSizeofArray + 1))
        lblAverage.Visible = True
        lblAverage.Text = intAverage
        Array.Sort(intGrades)

        intCount = 0

        'Writes the grades and average into the text file
        If IO.File.Exists(strLocationandFileName) Then
            For intCount = 0 To intSizeofArray
                objWriter.WriteLine(CInt(intGrades(intCount)))
            Next
            objWriter.WriteLine(intAverage)
        End If
        objWriter.Close()
    End Sub
    Private Function fncValidateGrade()
        'More variables
        Dim strGradesInputMessage As String = "Enter grade #"
        Dim strGradesInputHeading As String = "Grades"
        Dim blnValidityCheck As Boolean = False
        Dim strInputEntry As String
        Dim strCount As String
        'Get the grade from an input box, convert it, and make sure it is a number between 1-100
        intInputEntry = Convert.ToString(intInputEntry)
        strInputEntry = intInputEntry
        strCount = intCount
        strGrades(strCount) = InputBox(strGradesInputMessage & strInputEntry, strGradesInputHeading)
        If strGrades(intCount) = "" Then
            strGrades(intCount) = Convert.ToInt32(intGrades(intCount))
            intGrades(intCount) = strGrades(intCount)
            intCount = 9
            blnValidityCheck = True
        Else
            Try
                strGrades(intCount) = Convert.ToInt32(strGrades(intCount))
                intGrades(intCount) = strGrades(intCount)
                If intGrades(intCount) >= 0 And intGrades(intCount) <= 100 Then
                    blnValidityCheck = True
                Else
                    MsgBox("Please enter a grade between 0-100",, "Error")
                End If
            Catch ex As FormatException
                MsgBox("Please enter a grade between 0-100",, "Error")
            Catch ex As OverflowException
                MsgBox("Please enter a grade between 0-100",, "Error")
            Catch ex As SystemException
                MsgBox("Please enter a grade between 0-100",, "Error")
            End Try
        End If
        Return blnValidityCheck
    End Function

    Private Sub frmFinal_Load(sender As Object, e As EventArgs) Handles MyBase.Load

    End Sub
End Class
